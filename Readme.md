## Bitwarden Backup and Decryption Scripts

### Overview
This repository contains two scripts: `bitwarden-backup` and `bitwarden-lister`. The `bitwarden-backup` script is designed to back up your Bitwarden vault, while `bitwarden-lister` allows you to list and decrypt your encrypted backups. These scripts are primarily for backup purposes and should not be relied upon for secure storage of sensitive data.

### Features
- `bitwarden-backup`: Backs up your Bitwarden vault and encrypts the backup using AES-256-CBC.
- `bitwarden-lister`: Lists your encrypted backup files and allows you to select one for decryption. This script does not require a password to run.
- You can use `openssl` for decryption directly if you prefer not to use `bitwarden-lister`.

### Prerequisites
- **OpenSSL**: Ensure `openssl` is installed on your system for encryption and decryption.
- **Bitwarden-Cli** Enusre you have `bw` So you can interact with Bitwarden
- **jq** (Optional): Used for verifying the integrity of the decrypted JSON file.
- **fzf** (Optional): Provides interactive file selection in `bitwarden-lister`. If not installed, the script will list files for manual selection.

###  Usage
1. **Set up**: Define your `MASTER_KEY` and `BACKUP_DIR` in both scripts. Make sure to adjust the paths as necessary.
2. **Run the Scripts**:
   - For backing up your Bitwarden vault: `./bitwarden-backup`
   - For listing and decrypting backups: `./bitwarden-lister` (make sure both of them have the same dir if you want to change it )
3. **OpenSSL Decryption**: If you prefer not to use `bitwarden-lister`, you can decrypt files directly using OpenSSL:
   `openssl enc -d -aes-256-cbc -in "your_encrypted_file_name.enc" -out "decrypted_file_name.json" -pass pass:"your_master_key"`
4. **Make Scripts Executable and Accessible**: You can encrypt the scripts with `shc` for added protection:
   `shc -f bitwarden-backup`
   `shc -f bitwarden-lister`
   Place the resulting executables ` bitwarden-backup.x/bitwarden-lister.x` in `/bin` or `/usr/bin` for global access.
5. **Autostart Setup**: To ensure the scripts run automatically, you may want to add them to your bash profile (`~/.bashrc` or `~/.bash_profile`):
   `# Add these lines to your ~/.bashrc or ~/.bash_profile`
   `alias backup_bitwarden='bitwarden-backup'`( This is just an example you can make them any way or form autostart like WM add them to your config or DE make a seperet script just saying this script is made to be started without human interaction  )

### Security Note
These scripts are intended for backup purposes only. While they utilize encryption, relying solely on scripts for security is not advisable. Make sure to encrypt your device and follow best security practices. Always manage your sensitive data carefully and consider additional layers of security beyond these scripts.

### Logs
Decryption errors are logged in `$BACKUP_DIR/decrypt.log`.

### Cleaning Up
To avoid leaving session files or sensitive information, the scripts ensure proper clean-up after every run.
