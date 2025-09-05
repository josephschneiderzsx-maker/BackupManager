# Backup Manager

A simple tool to automatically back up MySQL databases on a schedule.

## Requirements

*   Windows Operating System (x64)
*   [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
*   MySQL Server or MySQL Client Tools must be installed. The backup tool requires access to `mysql.exe` and `mysqldump.exe`.

## Installation and Setup

1.  Place the application folder on the computer you want to run backups from.
2.  *   Run `BackupManager.exe` from an **elevated command prompt** (Run as administrator).
3.  On the first run, a setup wizard will launch in the command-line window. You will only need to do this once.
4.  Follow the prompts to configure your database connection, license, and backup schedule.

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
