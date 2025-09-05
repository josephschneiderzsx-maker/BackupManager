# Backup Manager

A simple tool to automatically back up MySQL databases on a schedule.

## Requirements

*   Windows Operating System (x64)
*   [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
*   MySQL Server or MySQL Client Tools must be installed. The backup tool requires access to `mysql.exe` and `mysqldump.exe`.

## Installation and Setup

*   To ensure proper functionality and performance, we recommend placing the application folder in a location without spaces in the path, such as C:\BackupManager. This can help avoid potential issues with command-line execution.
*   Extract and Place the Folder: Move or copy the extracted BackupManager folder to a simple path like C:\ to get a path like C:\BackupManager.
*   Run with Administrator Privileges: Open an elevated command prompt (Run as administrator) and navigate to the application folder.
*   Initial Setup Wizard: On the first run, execute BackupManager.exe. A setup wizard will guide you through the configuration.
*   Follow Prompts: Configure your license, database connection, MySQL binaries path, and backup schedule.

## Advanced User Configuration

*   For advanced users, adding the application's directory to the Windows Environment Variables simplifies command-line usage. This allows you to run BackupManager.exe with its arguments from any terminal without needing to navigate to the folder first. This is particularly useful for re-running the setup (--setup) or performing a manual backup (--run-now) from an administrator-level command prompt.

## To add the path:

*   Search for "Edit the system environment variables" in the Windows Start Menu.
*   Click on Environment Variables.
*   Under System variables, select the Path variable and click Edit.
*   Click New and add the full path to your BackupManager folder (e.g., C:\BackupManager).
*   Click OK on all windows to save the changes.

### Configuration Details

The setup wizard will ask for the following information:

*   **Company ID & Subscription Key**: Your license information for the application.
*   **Database Connection**: The host, username, password, and database name for the MySQL database you want to back up.
*   **MySQL Binaries Path**: This is the most critical step. You must provide the **full path** to the `bin` directory of your MySQL installation. The application needs this to find the `mysql.exe` and `mysqldump.exe` command-line tools.
    *   **Example Path**: `C:\Program Files\MySQL\MySQL Server 8.0\bin`
*   **Backup Storage Path**: The folder where your `.sql` backup files will be saved.
    *   If you press `Enter`, it will default to a `Backups` folder created inside the application directory.
*   **Backup Schedule**: How often (Daily, Weekly, etc.) and at what time the backups should occur. The application will automatically create a task in the Windows Task Scheduler to manage this.

## Usage

Once setup is complete, the application will run automatically on the schedule you defined.

### Command-Line Arguments

You can run the executable with arguments for specific actions:

*   **Run a Manual Backup**: To perform a backup immediately, run the program with the `--run-now` argument.
    ```sh
    BackupManager.exe --run-now
    ```
*   **Re-run Setup**: To change your configuration, run the program with the `--setup` argument. This will launch the setup wizard again.
    ```sh
    BackupManager.exe --setup
    ```

## Logging

The application logs its activity (e.g., successful backups, errors) to the **Windows Event Log**.

*   Open Event Viewer.
*   Go to **Windows Logs > Application**.
*   Look for events with the source name **BackupManager**.
