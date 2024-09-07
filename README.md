# Foundations_Computer_System

# *** Task 1 : Set Up Project Directory Structure

1. Create the Project directory in your home directory:
mkdir ~/Project

2. Navigate into the Project directory:
cd ~/Project

3. Create the subdirectories src, docs, and bin
mkdir src docs bin

4. Navigate into the src directory:
cd src

5. Create the files main.c, utils.c, and Makefile:
touch main.c utils.c Makefile

6. Move Makefile to the bin directory
mv Makefile ../bin/

7. Rename main.c to program.c
mv main.c program.c

8. Copy program.c to the docs directory:
cp program.c ../docs/

9. Verify the directory structure by listing the contents recursively:
ls -R ~/Project

# *** Task 2: Shell Script to Delete Empty Files
# Create a shell script named deleteEmptyFilesWithLog.sh:

#!/bin/bash
# Prompt user for directory path
read -p "Enter the directory path: " dir_path
# Validate if the directory path is valid
if [ ! -d "$dir_path" ]; then
    echo "The path $dir_path is not a valid directory."
    exit 1
fi
# Initialize the log file
log_file="deletedfiles.txt"
> "$log_file"
# Find and delete empty files, log their names
find "$dir_path" -type f -empty -print -exec rm {} \; > "$log_file"
# Print the list of deleted files
if [ -s "$log_file" ]; then
    echo "Deleted files:"
    cat "$log_file"
else
    echo "No empty files were found."
fi
# Clean up by removing the log file
rm "$log_file"
***Make the script executable and run it:
chmod +x deleteEmptyFilesWithLog.sh
./deleteEmptyFilesWithLog.sh


# *** Task 3: Shell Script to Calculate Total Size of Files
# *** Create a shell script named calculateSize.sh:
#!/bin/bash
# Check if a directory path is provided
if [ $# -ne 1 ]; then
    echo "Usage: $0 <directory_path>"
    exit 1
fi

dir_path="$1"

# Validate if the directory path exists
if [ ! -d "$dir_path" ]; then
    echo "The path $dir_path does not exist."
    exit 1
fi

# Calculate the total size of all files in the directory
total_size=$(find "$dir_path" -maxdepth 1 -type f -exec du -ch {} + | grep total$ | awk '{print $1}')

# Print the total size
echo "Total size of files in $dir_path: $total_size"

Make the script executable and run it:
chmod +x calculateSize.sh
./calculateSize.sh /path/to/directory

# *** Task 4: Shell Script for CPU and Memory Usage Report
# *** Create a shell script named resourceReport.sh: 

#!/bin/bash

# Create or clear the resource report file
report_file="resourceReport.txt"
> "$report_file"

# Generate the report
ps aux --sort=-%cpu | awk '{print $1, $2, $3, $4, $11}' > "$report_file"

# Print a success message
echo "Resource report has been saved to $report_file."

Make the script executable and run it:
chmod +x resourceReport.sh
./resourceReport.sh

# *** Task 5: Shell Script for Disk Usage, File Listing, and Free Memory
# *** Create a shell script named fileSummary.sh:
#!/bin/bash

# Print disk usage of the root directory
echo "Disk usage of /:"
df -h /

# List all files in the current directory
echo "Files in the current directory:"
ls -p | grep -v /

# Display free memory available on the system
echo "Free memory available:"
free -h

Make the script executable and run it:
chmod +x fileSummary.sh
./fileSummary.sh

