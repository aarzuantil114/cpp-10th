#include <iostream>
#include <fstream>
#include <cstdlib>

using namespace std;

// Function to report kernel version
void reportKernelVersion() {
    cout << "Kernel Version:" << endl;
    system("uname -r");  // Executes the 'uname -r' command to fetch the kernel version
    cout << endl;
}

// Function to report CPU type and information
void reportCPUTypeAndInfo() {
    cout << "CPU Type and Information:" << endl;

    // Open and read the /proc/cpuinfo file
    ifstream cpuInfoFile("/proc/cpuinfo");
    if (cpuInfoFile.is_open()) {
        string line;
        while (getline(cpuInfoFile, line)) {
            // Filter and display relevant CPU details
            if (line.find("model name") != string::npos || 
                line.find("vendor_id") != string::npos || 
                line.find("cpu cores") != string::npos) {
                cout << line << endl;
            }
        }
        cpuInfoFile.close();
    } else {
        cerr << "Error: Unable to open /proc/cpuinfo file." << endl;
    }

    cout << endl;
}

int main() {
    // Report kernel version
    reportKernelVersion();

    // Report CPU type and information
    reportCPUTypeAndInfo();

    return 0;
}
