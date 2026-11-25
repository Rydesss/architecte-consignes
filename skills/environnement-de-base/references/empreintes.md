# Empreintes : contrôle des copies

Ce fichier donne les commandes exactes du contrôle par empreintes : pas 7 de la partie B de [stockage.md](stockage.md) (étape 5 du `SKILL.md` de ce skill), et points 1 et 2 de son Test (étape 10). Les règles de la copie, la liste des exclus (pas 4) et le traitement des écarts (pas 8) restent dans `stockage.md`. Sous Windows, lancer ces commandes avec l'outil PowerShell de Claude Code (`stockage.md`, en tête). Elles n'écrivent que dans `<journal>`. Un « pas » renvoie à la partie B de `stockage.md`.

Mot à dire au premier usage, s'il ne l'a pas été : « Une empreinte est un code calculé à partir du contenu d'un fichier : deux fichiers de même empreinte ont, en pratique, le même contenu. »

## Contrôle d'un lot

- Les commandes ci-dessous lisent les deux côtés en entier, puis les comparent. Un dossier exclu n'est pas parcouru, et aucun de ses fichiers n'est lu. Les fichiers que le système crée de lui-même (`.DS_Store`, `desktop.ini`, `Thumbs.db`) sont écartés des deux côtés : ils ne sortent jamais en écart.
- Listes de référence (`empreintes-<Lot>-source` et `empreintes-<Lot>-copie`) : enregistrées dans `<journal>` seulement si la comparaison ne trouve aucun écart. Ce sont celles du dernier contrôle réussi ; le Test de l'étape 10 s'y compare. Avec un écart, elles ne changent pas : les deux listes du passage vont dans des listes de diagnostic à part (`ecart-<Lot>-source` et `ecart-<Lot>-copie`), et le lot reste « non vérifié » tant qu'aucun contrôle n'a abouti sans écart.
- Toute erreur arrête le contrôle avant tout enregistrement : fichier verrouillé ou illisible, dossier refusé, chemin absent, lien ou jonction non exclu. Les listes déjà enregistrées restent alors intactes.
- Chemins écartés de la comparaison, à reporter avant tout calcul : les exclus du pas 4, plus les fichiers que le participant a modifiés ou ajoutés dans la copie, et ceux dont l'original a disparu de la source, notés au pas 8 (leur original n'est alors plus vérifié ; le dire). Windows, dans `$x` : les chemins relatifs entre apostrophes, séparés par des virgules (`@()` sans chemin). macOS, dans `<exclusions>` : `\( -ipath './<chemin relatif>' -o -ipath './<autre chemin relatif>' \) -prune -o` (rien sans chemin).

```powershell
$ErrorActionPreference = 'Stop'
function Get-Empreintes([string]$Racine, [string[]]$Exclus = @()) {
  $base = (Resolve-Path -LiteralPath $Racine -ErrorAction Stop).ProviderPath.TrimEnd('\')
  $ex = @($Exclus | ForEach-Object { $_.Replace('/', '\').Trim('\') } | Where-Object { $_ })
  $pile = New-Object System.Collections.Stack; $pile.Push($base)
  while ($pile.Count) {
    foreach ($e in @(Get-ChildItem -LiteralPath $pile.Pop() -Force -ErrorAction Stop)) {
      $c = $e.FullName.Substring($base.Length + 1)
      if ($e.Name -in '.DS_Store', 'desktop.ini', 'Thumbs.db') { continue }
      if ($ex | Where-Object { $c -eq $_ -or $c.StartsWith("$_\", [StringComparison]::OrdinalIgnoreCase) }) { continue }
      if ($e.LinkType) { throw "lien ou jonction non exclu : $c" }
      if ($e.PSIsContainer) { $pile.Push($e.FullName); continue }
      $h = (Get-FileHash -LiteralPath $e.FullName -Algorithm SHA256 -ErrorAction Stop).Hash
      if ($h -notmatch '^[0-9A-F]{64}$') { throw "empreinte illisible : $c" }
      [pscustomobject]@{ Chemin = $c; SHA256 = $h } } }
}
function Compare-Empreintes($Reference, $Copie) {
  $r = @{}; $d = @{}
  foreach ($l in @($Reference | Where-Object { $_ })) { if ($l.SHA256 -notmatch '^[0-9A-F]{64}$') { throw "liste invalide : $($l.Chemin)" }; $r[$l.Chemin] = $l.SHA256 }
  foreach ($l in @($Copie | Where-Object { $_ })) { if ($l.SHA256 -notmatch '^[0-9A-F]{64}$') { throw "liste invalide : $($l.Chemin)" }; $d[$l.Chemin] = $l.SHA256 }
  foreach ($c in $r.Keys) { if (-not $d.ContainsKey($c)) { "manquant dans la copie : $c" } elseif ($d[$c] -ne $r[$c]) { "différent : $c" } }
  foreach ($c in $d.Keys) { if (-not $r.ContainsKey($c)) { "en plus dans la copie : $c" } }
}
$j = "<journal>"; $x = @('<chemin relatif exclu>')
try { $s = @(Get-Empreintes "<source>" $x); $d = @(Get-Empreintes "<destination>" $x) }
catch { throw "Contrôle interrompu, copie NON vérifiée : $($_.Exception.Message)" }
$e = @(Compare-Empreintes $s $d)
if ($e.Count -eq 0) {
  $s | Export-Csv -LiteralPath "$j\empreintes-<Lot>-source.csv" -NoTypeInformation -Encoding UTF8
  $d | Export-Csv -LiteralPath "$j\empreintes-<Lot>-copie.csv" -NoTypeInformation -Encoding UTF8
  "Aucun écart : $($s.Count) fichier(s) de chaque côté. Listes de référence enregistrées : lot vérifié."
} else {
  $s | Export-Csv -LiteralPath "$j\ecart-<Lot>-source.csv" -NoTypeInformation -Encoding UTF8
  $d | Export-Csv -LiteralPath "$j\ecart-<Lot>-copie.csv" -NoTypeInformation -Encoding UTF8
  $e; "$($e.Count) écart(s). Listes de référence inchangées ; diagnostic : ecart-<Lot>-source.csv et ecart-<Lot>-copie.csv. Lot non vérifié."
}
```

```sh
set -o pipefail; j="<journal>"
if s=$(cd "<source>" && find . \( -iname .DS_Store -o -iname desktop.ini -o -iname Thumbs.db \) -prune -o <exclusions> -type f -exec shasum -a 256 {} + | LC_ALL=C sort -k 2) &&
   c=$(cd "<destination>" && find . \( -iname .DS_Store -o -iname desktop.ini -o -iname Thumbs.db \) -prune -o <exclusions> -type f -exec shasum -a 256 {} + | LC_ALL=C sort -k 2); then
  if [ "$s" = "$c" ]; then
    if printf '%s\n' "$s" > "$j/empreintes-<Lot>-source.txt" && printf '%s\n' "$c" > "$j/empreintes-<Lot>-copie.txt"; then
      echo "Aucun écart : $(printf '%s' "$s" | grep -c .) fichier(s) de chaque côté. Listes de référence enregistrées : lot vérifié."
    else echo "Aucun écart, mais listes de référence NON enregistrées (journal absent ou non accessible en écriture) : lot non vérifié. Créer <journal> (partie B), puis refaire le pas 7."; fi
  else
    printf '%s\n' "$s" > "$j/ecart-<Lot>-source.txt"; printf '%s\n' "$c" > "$j/ecart-<Lot>-copie.txt"
    diff "$j/ecart-<Lot>-source.txt" "$j/ecart-<Lot>-copie.txt"
    echo "Écarts ci-dessus. Listes de référence inchangées ; diagnostic : ecart-<Lot>-source.txt et ecart-<Lot>-copie.txt. Lot non vérifié."
  fi
else echo "Contrôle interrompu, copie NON vérifiée : lire l'erreur ci-dessus."; fi
```

## Lecture du résultat

- Attendu : « Aucun écart », le nombre de fichiers, puis « lot vérifié ». Sinon, chaque écart est listé (pas 8) : Windows, « manquant dans la copie », « en plus dans la copie » ou « différent » ; macOS, une ligne `<` est manquante dans la copie, `>` en plus dans la copie, et un chemin des deux côtés est un fichier différent. Après correction des écarts, refaire le pas 7 jusqu'à « lot vérifié ».
- « Aucun écart : 0 fichier(s) » : aucun fichier autorisé dans le lot. Le dire, et vérifier avec (U) que tout le lot est bien exclu.
- « Contrôle interrompu » : jamais « empreintes identiques ». Lire l'erreur, corriger la cause (fichier ouvert dans une application, fichier encore en ligne seulement, lien à ajouter aux exclus du pas 4), puis refaire le pas 7.
- `.DS_Store`, `desktop.ini` et `Thumbs.db` : écartés par les commandes, des deux côtés. Un exclu du pas 4 qui sort « manquant » a été oublié dans `$x` ou `<exclusions>`, donc lu : le dire au participant, l'y ajouter sans le recopier, refaire le pas 7.

## Test de l'étape 10

Originaux intacts (point 1) : recalculer les empreintes de la source et les comparer à la liste de référence de la source. Ces commandes n'écrivent rien. Lot jamais vérifié (pas de liste de référence) : le dire ; refaire d'abord le pas 7.
- Windows : en tête de la commande, reprendre de « Contrôle d'un lot » la ligne `$ErrorActionPreference`, les deux fonctions, `$j` et `$x`, puis `$e = @(Compare-Empreintes (Import-Csv -LiteralPath "$j\empreintes-<Lot>-source.csv") (Get-Empreintes "<source>" $x)); $e; "Écarts : $($e.Count)."`
- macOS : `set -o pipefail; j="<journal>"; if n=$(cd "<source>" && find . \( -iname .DS_Store -o -iname desktop.ini -o -iname Thumbs.db \) -prune -o <exclusions> -type f -exec shasum -a 256 {} + | LC_ALL=C sort -k 2); then printf '%s\n' "$n" | diff "$j/empreintes-<Lot>-source.txt" - && echo "Aucune différence."; else echo "Contrôle interrompu : originaux NON vérifiés."; fi`
- Attendu : « Écarts : 0 » (macOS : « Aucune différence »). Ici, « manquant dans la copie » signale un original disparu ou déplacé, « en plus » un original ajouté, « différent » un original modifié, par Claude ou par un collaborateur en ligne : regarder avec le participant. Une erreur : originaux non vérifiés, à noter à « À confirmer ».

Copie (point 2) : la comparer de même à la liste de référence de la source, avec les mêmes chemins écartés (Windows : `Get-Empreintes "<destination>" $x` à la place de la source ; macOS : `cd "<destination>"`). Attendu : aucun écart, sauf les fichiers que le participant a modifiés ou ajoutés depuis.

## Limites

- Windows : commandes rejouées telles quelles sur des dossiers fictifs locaux (Sources). Pas encore sur un vrai dossier OneDrive ou Google Drive.
- macOS : commandes déduites, non testées (`-ipath`, `-prune`, `pipefail`, code de sortie de `shasum` sur un fichier illisible).
- Les empreintes lisent le contenu entier des fichiers : un fichier encore en ligne seulement est téléchargé pendant le calcul (`stockage.md`, partie B, pas 2).

## Sources

Observés le 25/11/2026 en relecture (Windows 11, dossiers fictifs) : reprise d'un `robocopy` réellement interrompu (fichier partiel gardé, pièces manquantes récupérées, réparation ciblée, relance code 0) ; ancienne fonction d'empreintes trompée par une exclusion écrite dans une autre casse, et par deux fichiers verrouillés (empreintes vides, aucune différence signalée). Observés le 25/11/2026 sur banc fictif (Windows PowerShell 5.1) : exclusions `/XF` et `/XD` écrites dans une autre casse respectées par `robocopy` ; fonction actuelle arrêtée par un fichier verrouillé, un dossier refusé, un chemin absent et une liste à empreinte vide ; lot entièrement exclu compté zéro de chaque côté ; `$ErrorActionPreference = 'Stop'` sans effet sur l'erreur de lecture de `Get-FileHash`, d'où `-ErrorAction Stop` écrit dans la commande. Rejouées le 25/11/2026, sur un banc fictif, telles qu'écrites ici : copie intacte (aucun écart), original modifié (« différent »), fichier verrouillé (contrôle interrompu, listes enregistrées intactes), dossier exclu écrit dans une autre casse (absent de la copie et des listes) ; un `/XD` écrit avec `/` n'exclut rien. Observé le 25/11/2026 en relecture (PowerShell 7.6.9, dossiers fictifs) : la version précédente remplaçait les listes de référence par celles d'un passage avec écart. Rejoué le 25/11/2026 avec la version actuelle, telle qu'écrite (Windows PowerShell 5.1, six lots fictifs, 32 vérifications réussies) : après un écart dans la copie ou dans la source, listes de référence inchangées et diagnostic à part ; Test de l'étape 10 qui voit l'original modifié ; verrou puis déverrouillage sans changement des listes de référence ; lot entièrement exclu ; `desktop.ini` et `.DS_Store` ajoutés à la copie sans écart ; fichier en plus signalé, puis écarté de la comparaison. Logique du bloc sh rejouée sous Git Bash (GNU find, `sha256sum` à la place de `shasum -a 256`) : journal absent signalé « NON enregistrées », exclu écrit dans une autre casse, `.DS_Store` écarté, écart sans changement de la liste de référence ; BSD find de macOS non essayé.
- Options de `robocopy` : sources de [stockage.md](stockage.md). Code de sortie de `find … -exec … +` et de `shasum` sous macOS : déduits, non vérifiés dans une documentation.
