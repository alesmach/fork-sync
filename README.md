# fork-sync

Každý den synchronizuje všechny moje forky s jejich původními repozitáři (`gh repo sync`).
Ve forcích samotných jsou GitHub Actions vypnuté, běží jen tady.

## Nastavení

1. Vytvoř fine-grained token: <https://github.com/settings/personal-access-tokens/new>
   - **Repository access:** All repositories (pak se automaticky zahrnou i nové forky)
   - **Permissions → Repository:** Contents = Read and write, Workflows = Read and write
     (Metadata = Read se přidá samo)
2. Ulož ho jako secret `FORK_SYNC_TOKEN`:
   `gh secret set FORK_SYNC_TOKEN -R alesmach/fork-sync`
3. Spusť ručně: `gh workflow run sync.yml -R alesmach/fork-sync`

## Poznámky

- Sync jen posouvá větev dopředu. Pokud má fork na hlavní větvi vlastní commity, sync selže
  a nic nepřepíše.
- Forky, které se synchronizovat nemají, jsou v proměnné `SKIP` v `.github/workflows/sync.yml`.
- Když sync selže, běh skončí chybou a GitHub pošle e-mail. Přehled je v souhrnu běhu.
