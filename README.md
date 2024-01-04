Sharuf Zaryab Khan 231633.
Course: Programming Fundamentals
Instructor: Dr. Ashfaq Hussain Farooqi
Class: BSCS-IB
Project: Clothes Management System

Code:

#include <iostream> // Header files...
#include <fstream>
#include <string>
using namespace std;
// Functions
void addclothes(); // void is function that gives no retrun values if program is sucessfully terminated
void viewrecord();
void searchrecord();
void updaterecord();
void deleterecord();
void exitrecord();
int main() {
 int choice; // For use of switch...
 cout << "Cloth Management System\n";
 cout << "1. Add Clothes\n"; // for addrecord function...
 cout << "2. Search Record\n"; // for searchrecord function
 cout << "3. View Records\n"; // for viewrecord function
 cout << "4. Update/edit Record\n"; // for updaterecord funtion
 cout << "5. Delete Record\n"; // delete record option
 cout << "6. Exit\n"; // exit option
 cout << "Enter your choice: ";
 cin >> choice;
 switch (choice) {
 case 1:
 addclothes();
 break;
 case 2:
 searchrecord();
 break;
 case 3:
 viewrecord();
 break;
 case 4:
 updaterecord();
 break;
 case 5:
 deleterecord();
 break;
 case 6:
 exitrecord();
 break;
 
 default:
 cout << "incorrect choice \n"; // for invalid input.
 }
 return 0;
}
void addclothes() {
 ofstream fout; // for writhig to file...
 fout.open("ClothManagementSystem.txt", ios::app);// ios::app for apendding any data 
 int clothid, quantity, price;
 string clothname;
 cout << "Enter Cloth Id\n";
 cin >> clothid;
 cout << "Enter price\n";
 cin >> price;
 cout << "Enter quantity\n";
 cin >> quantity;
 cout << "Enter cloth name\n";
 cin >> clothname;
 fout << clothid << " " << clothname << " " << quantity << " " << price << endl; // saving data in 
file...
 fout.close(); // closing file...
}
void searchrecord() {
 ifstream fin;
 fin.open("ClothManagementSystem.txt"); //reading the file...
 int clothid, clothidinfile, quantity, price;
 string clothname;
 bool found = false; //boolean variable found is assigned false.
 cout << "Enter id to search its record \n";
 cin >> clothid;
 while (fin >> clothidinfile >> clothname >> quantity >> price) {
 if (clothidinfile == clothid) {
 found = true; //if clothidinfile matches clothid found is cahnged to true
 cout << clothid << " exists in the record with details:\n";
 cout << "Cloth Name: " << clothname << endl;
 cout << "Quantity: " << quantity << endl;
 cout << "Price: " << price << endl;
 break; // to exit the loop...
 }
 }
 if (!found) { //!found is a logical NOT operator it changes the value of found...
 cout << clothid << " does not exist in the record.\n";
 }
 fin.close();
}
void viewrecord() {
 ifstream fin; // for reading the file...
 fin.open("ClothManagementSystem.txt");
 int clothid, quantity, price;
 string clothname;
 cout << "Cloth ID\tCloth Name\tQuantity\tPrice\n"; // fot aligning the text.
 while (fin >> clothid >> clothname >> quantity >> price) {
 cout << clothid << "\t\t" << clothname << "\t\t" << quantity << "\t\t" << price << endl;// for 
aligning the text above 
 }
 fin.close();
}
void updaterecord() {
 ifstream fin;
 ofstream fout;
 fin.open("ClothManagementSystem.txt");
 fout.open("Temp.txt", ios::app); // ios::app means any data written to file is added to the existing 
content. 
 int clothid, clothidinfile, quantity, price;
 string clothname;
 bool found = false; // assignig value to boolian found false
 cout << "Enter id to update its record \n";
 cin >> clothid;
 while (fin >> clothidinfile >> clothname >> quantity >> price) {
 if (clothidinfile == clothid) {
 found = true; // assignig value to boolian found true
 cout << "Enter updated details for the record:\n";
 cout << "New Cloth Name: ";
 cin >> clothname;
 cout << "New Quantity: ";
 cin >> quantity;
 cout << "New Price: ";
 cin >> price;
 fout << clothid << " " << clothname << " " << quantity << " " << price << endl;
 cout << "Record updated successfully.\n";
 }
 else {
 fout << clothidinfile << " " << clothname << " " << quantity << " " << price << endl;
 }
 }
 if (!found) { //!found is a logical NOT operator it changes the value of found...
 cout << clothid << " does not exist in the record.\n";
 }
 fin.close();
 fout.close();
 remove("ClothManagementSystem.txt"); // Removing the old file
 rename("Temp.txt", "ClothManagementSystem.txt"); //renaming the temporary file
}
void exitrecord()
{
 cout << "Exiting from the system...";
 exit(0);
}
void deleterecord() {
 ifstream fin;
 ofstream fout;
 fin.open("ClothManagementSystem.txt"); // creating file
 fout.open("Temp.txt", ios::app); // ios::app means any data written to file is added to the existing 
content. 
 int clothid, clothidinfile, quantity, price;
 string clothname;
 bool found = false; // assignig value to boolian found false....
 cout << "Enter id to delete its record \n";
 cin >> clothid;
 while (fin >> clothidinfile >> clothname >> quantity >> price) {
 if (clothidinfile == clothid) {
 found = true; // assignig value to boolian found true
 cout << "Record with id " << clothid << " is deleted successfully.\n";
 }
 else {
 fout << clothidinfile << " " << clothname << " " << quantity << " " << price << endl;
 }
 }
 if (!found) {
 cout << clothid << " does not exist in the record.\n";
 }
 fin.close();
 fout.close();
 // romoving the old file and renaming the temporary file
 remove("ClothManagementSystem.txt");
 rename("Temp.txt", "ClothManagementSystem.txt");
}