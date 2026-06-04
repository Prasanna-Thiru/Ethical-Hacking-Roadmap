# 📂 File System  

• Linux organizes everything into a hierarchical tree structure starting at / (root).  

Common directories:  

•  /home → personal files for each user.  

• /etc → system configuration files.  

• /bin → essential system commands.  

• /var → logs and variable data.  

• /tmp → temporary files.  

• Unlike Windows, Linux doesn’t use drive letters (C:, D:). Instead, all devices are mounted into this single tree.  

# 🔑 Permissions  

• Every file/directory has three types of permissions:  

    • Read (r) → view contents.

    • Write (w) → modify or delete.

    • Execute (x) → run as a program/script.

• Permissions apply to:  

    • Owner (the user who created the file).

    • Group (a set of users).

    • Others (everyone else).

• Example: -rw-r--r--  

    • Owner: read/write

    • Group: read

    • Others: read

• Commands:  

    • ls -l → view permissions.

    • chmod → change permissions.

    • chown → change ownership.  

# 👥 Users & Groups

• Users: Each person/system process has a unique account.

• Groups: Collections of users with shared permissions.

• Types of users:

    • Root → superuser with full control.

    • Regular users → limited access.

• Important files:

    • /etc/passwd → user account info.

    • /etc/group → group info.

• Commands:

    • adduser username → create user.

    • passwd username → set/change password.

    • usermod -aG group username → add user to group.

🛠️ File Operations

• Navigation:

    • pwd → show current directory.

    • cd → change directory.

• Listing:

    • ls → list files.

    • ls -l → detailed view.

• Creation:

    • touch file.txt → create empty file.

    • mkdir folder → create directory.

• Copy/Move/Delete:

    • cp source destination → copy.

    • mv source destination → move/rename.

    • rm file.txt → delete file.

    • rm -r folder → delete folder recursively.

• Viewing contents:

    • cat file.txt → show contents.

    • less file.txt → scroll through file.

    • head -n 10 file.txt → first 10 lines.

    • tail -n 10 file.txt → last 10 lines.•