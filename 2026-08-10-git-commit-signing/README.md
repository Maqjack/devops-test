# Zadanie domowe 10.08 - podpisywanie commitow kluczem SSH

Tresc zadania (Slack, Patryk Trautberg): dostosowanie git config, aby podpisywal commit'y wygenerowanym kluczem SSH.

## Wykonane kroki

1. Wygenerowanie dedykowanego klucza SSH do podpisywania:
   ssh-keygen -t ed25519 -C "maciek.jackowicz@gmail.com-git-signing" -f ~/.ssh/id_ed25519_git_signing -N ""

2. Konfiguracja git do uzywania formatu SSH zamiast GPG:
   git config --global gpg.format ssh
   git config --global user.signingkey ~/.ssh/id_ed25519_git_signing.pub
   git config --global commit.gpgsign true

3. Plik allowed_signers do lokalnej weryfikacji podpisow:
   mkdir -p ~/.config/git
   echo "USER_EMAIL PUBLIC_KEY" > ~/.config/git/allowed_signers
   git config --global gpg.ssh.allowedSignersFile ~/.config/git/allowed_signers

## Weryfikacja

Klucz publiczny uzyty do podpisywania: id_ed25519_git_signing.pub w tym katalogu.
Commit'y w tym repozytorium sa podpisane tym kluczem - widoczne w "git log --show-signature".
