# 📦 Moving WSL Distribution to Another Drive

🚀 This guide explains the process of moving a Linux distribution installed on Windows Subsystem for Linux (WSL) to another drive. In this example, we will be moving an Ubuntu 22.04 distribution, and the steps are outlined below.

## 🛠️ Prerequisites

- Windows operating system with WSL 2 installed.

## 📋 Instructions

1. **Check the existing WSL installations**  
   Run the following command in a WSL or Command Prompt window to view your current WSL distributions and their versions:

   ```bash
   wsl --list -v
   ```

   If the installation you want to move is currently running, stop it using the `wsl -t` command. For example:

   ```bash
   wsl -t Ubuntu-22.04
   ```

2. **Export the WSL distribution**  
   Export the distribution to a `.tar` file. For example, to export Ubuntu 22.04 as `ubuntu-ex.tar` to the `D:\wsl_export` directory:

   ```bash
   wsl --export Ubuntu-22.04 "D:\wsl_export\ubuntu-ex.tar"
   ```

3. **Unregister the existing WSL installation**  
   Remove the Ubuntu 22.04 distribution from the WSL list using:

   ```bash
   wsl --unregister Ubuntu-22.04
   ```

### 4. **Import the WSL Installation to a New Location**

To move the exported WSL distribution to a new folder, you need to import the `.tar` file created in the previous step. When you import a distribution, it can be set to either WSL version 1 or version 2. By default, if no version is specified, it may import as version 1. To explicitly ensure that it is imported as WSL version 2, you should use the `--version` flag.

#### **Command to Import**

Use the following command to import the WSL distribution:

```bash
wsl --import <distro_name> <install_location> <path_to_tar_file> --version 2
```

- **`<distro_name>`**: The name you want to assign to the imported distribution. This is how it will be referenced in the WSL list and commands.
- **`<install_location>`**: The folder path where you want the distribution to be installed. This is typically a location on the drive where you want to store the distribution, such as `D:\wsl_import\ubuntu`.
- **`<path_to_tar_file>`**: The path to the exported `.tar` file created earlier, e.g., `D:\wsl_export\ubuntu-ex.tar`.
- **`--version 2`**: Specifies that the distribution should be imported as WSL version 2.

#### **Example**

To import the Ubuntu 22.04 distribution to the folder `D:\wsl_import\ubuntu` using the exported `.tar` file `D:\wsl_export\ubuntu-ex.tar`, run:

```bash
wsl --import Ubuntu-22.04 "D:\wsl_import\ubuntu" "D:\wsl_export\ubuntu-ex.tar" --version 2
```

#### **Important Notes:**

- **Ensure the Target Directory Exists**: The target folder `D:\wsl_import\ubuntu` should either exist or be automatically created by the command. However, it's good practice to manually verify that the directory exists and is writable.
- **Specifying the Version**: If you do not include the `--version` flag, the imported distribution may default to version 1, especially if that was the default version for your WSL environment. Including `--version 2` ensures that the distribution will run as WSL 2, providing better performance and full system compatibility.
- **Checking Import Status**: After the import is complete, you can verify the success and version of the distribution using:
  ```bash
  wsl --list -v
  ```
  This command will show the current state and version of all registered WSL distributions.

- **Naming Conflicts**: Ensure the `<distro_name>` you choose does not conflict with existing distributions to avoid errors.

Following these steps ensures a smooth and precise import process with full control over the distribution’s version and location.

5. **Check and Set the WSL Version (if needed)**  
   Verify the version of your imported distribution using:

   ```bash
   wsl --list -v
   ```

   If the version shows as `1` instead of `2`, update it with the following command:

   ```bash
   wsl --set-version Ubuntu-22.04 2
   ```

6. **Set the Default User (optional)**  
   To avoid login prompts when launching the distribution, set the default user. Use the following command, replacing `me` with your actual username:

   ```bash
   ubuntu2204.exe config --default-user me
   ```

7. **Set the Default Distribution (optional)**  
   If you have multiple distributions registered and want the newly imported one to be the default, set it using:

   ```bash
   wsl --setdefault Ubuntu-22.04
   ```

🎉 **Congratulations!** You have successfully moved your WSL distribution to another drive and ensured it is running on WSL 2. You can now start the distribution and continue using it at the new location.



🛠️ Don't hesitate to create pull requests if you have suggestions for improvements to this guide. Your contributions are greatly appreciated!
