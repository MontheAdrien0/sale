// This is a program system for tracking sales
// bills from sales.

    #include<iostream>
    #include <fstream>
    #include <string>
    #include <vector>
    #include <iomanip>
	#include <fstream>
	#include <ostream>

	using namespace std;

	//Global variable for total of items entered
	int productsub[100];
	int productsadd[100];
	ofstream file;
	ifstream ifile;
	string filename;
	int out;
	float itemtotal;
	string itemspurchased;
	string date;
	char productname
	int productid;
	int itemsnum;
	int totalproducts;
	int defaultamount;
	int newamount;
	int price[9];
	int subproductsnum[100];
	int productsnum[100];
	int newproductsnum[100];
	string products[100] = {" "};

	//function prototypes
	void displaystock(); // 4.
	void defaultstock();
	void items(); // 1.
	void search();
	void exportfile();
	void menu();
	void addproducts();	// 2.
	void deleteproducts(); //5.
	void disstock();
	void viewstock();
	void addmoreproducts();

	int main()
	{
		char yes;
		system("cls");
		cout << " PIES Groceries sale Management System program\n";
		cout << " Press Any Key to Proceed\n";
		cin >> yes;
		system("cls");
		stock();

		return 0;
	}

	//Function for program stock
	void stock()
	{
		int stocknum;
		cout << "             stock             \n";
		cout << "            ******";
		cout << "\n\n1.Add Products to Stock\n";
		cout << "2.Add Sales Made(This would Make changes in your number of units)\n";
		cout << "3.Generate bill(Can only Generate a Bill for one Item purchased)\n";
		cout << "4.Display Current Stock & save Data to file\n";
		cout << "5.Display Old Stock and Display Last Data saved\n";
		cout << "6.Search Item in Stock\n";
		cout << "7.Exit Program\n\n";

		cout << "Enter your choice here:";
		cin >> stocknum;
		if (stocknum == 1)
		{
			system("cls");
			addproducts();

		}
		else if (stocknum == 2)
		{
			system("cls");
			items();
		}
		else if (stocknum == 3)
		{
			system("cls");
			cout << "What is Today's Date?\n";
			cout << "Enter here: ";
			cin.ignore();
			getline(cin, date);
			exportfile();
		}
		else if (stocknum == 4)
		{
			system("cls");
			displaystock();
		}
		else if (stocknum == 5)
		{
			system("cls");
			disstock();
		}
		else if (stocknum == 6)
		{
			system("cls");
			search();
		}
		else
		{
			system("cls");
			cout << "BYEEEEEE, HOPE TO SEE YOU AGAIN :)";
		}
	}

	//Function to Export data to file for printing
	void exportfile()
	{
		char exit;
		int itembought;
		string filename;
		ofstream file;
		cout << "What would you want the recent bill to be saved as? ";
		cin >> filename;
		system("cls");
		file.open(string(filename + ".txt").c_str());
		cout << "MilkID:0, RiceID:1, SugarID:2, ButterID:3, BreadID:4, MeatID:5, FishID:6, CerealID:7, CandyID:8\n";
		cout << "What was bought? Enter Product ID:";
		cin >> itembought;

		cout << "Writing to file...\n";
		cout << "About to finish...\n";
		file << "Product Bought: " << products[itembought] << "\n";
		file << "Amount to Pay: Php" << price[itembought] << "\n";
		file << "Date :" << date << "\n";
		file << "\nThank You for doing business with us, Hope to see you soon!";
		cout << "\nDone! You can print out the bill now!";
		file.close();

		cout << "Press any key & <enter> to skip to stock";
		cin >> exit;

		if (exit != '/')
		{
			stock();
		}
	}

	//function for adding products to stock
	void addproducts()
	{

		int choice;

		cout << "1. Add products to stock" << endl;
		cout << "2. Go to stock  " << endl;
		cout << "3. View Stock" << endl;
		cout << "4. Add more products" << endl;

		cout << "Enter here: ";
		cin >> choice;

		if (choice == 1)
		{

			system("cls");
			for (int p = 0; p < 9; p++)
			{
				cout << "\nEnter Amount of " << products[p] << ": ";
				cin >> productsnum[p];
				cout << "Enter price of " << products[p] << ": Php";
				cin >> price[p];
			}
		}
		else if (choice == 2)
		{
			stock();
		}
		else if (choice == 3)
		{
			viewstock();
		}
		else if (choice == 4)
		{
			addmoreproducts();
		}
		else
		{
			addproducts();
		}
		displaystock();
	}

	


	void calculatestock()
	{
		for (productid = 0; productid < 9; productid++)
		{
			productsnum[productid] = productsnum[productid] + newproductsnum[productid];
			subproductsnum[productid] = newproductsnum[productid] - productsub[productid];
		}
	}
	void displaystock()
	{
		cout << "ProductID\t\t"
		<< "Products"
		<< "\t"
		<< "Num of Products"
		<< "\t\t"
		<< "New Num of Products"
		<< "\tUnit Price" << endl;
		for (productid = 0; productid < 9; productid++)
		{
			subproductsnum[productid] = productsnum[productid] - productsub[productid];
			productsnum[productid] = productsnum[productid] + newproductsnum[productid];
			cout << productid << "\t\t\t" << products[productid] << "\t\t\t" << productsnum[productid] << "\t\t" << subproductsnum[productid] << "\t\t\t Php" << price[productid] << endl;
		}
		file.open("DefaultSTOCK");

		file << "ProductID\t\t"
		<< "Products"
		<< "\t"
		<< "Num of Products"
		<< "\t\t"
		<< "New Num of Products"
		<< "\t\tUnit Price" << endl;
		for (productid = 0; productid < 9; productid++)
		{
			file << productid << "\t\t\t" << products[productid] << "\t\t\t" << productsnum[productid] << "\t\t\t" << subproductsnum[productid] << "\t\t\t Php" << price[productid] << endl;
		}
		cout << "\nWriting to file...\n";
		cout << "Done writing new stock to file....\n";
		cout << "You file is automatically saved as ''DefualtSTOCK'' ";

		int out;
		cout << "press any number to proceed";
		cin >> out;
		if (out != 0)
		{
			stock();
		}
	}

	void disstock()
	{
		ifile.open("DefaultSTOCK");
		if (ifile.is_open())
		{
			string getcontent;
			while (getline(ifile, getcontent))
			{
				cout << getcontent << endl;
			}
		}
		int out;
		cout << "\n\npress any number to proceed";
		cin >> out;
		if (out != 0)
		{
			stock();
		}
	}
	void viewstock()
	{
		ifile.open("DefaultSTOCK");
		if (ifile.is_open())
		{
			string getcontent;
			while (getline(ifile, getcontent))
			{
				cout << getcontent << endl;
			}
		}
		int product_stock;
		cout << "\nPress any number to go to continue  ";
		cin >> product_stock;
		if (product_stock != 0)
		{
			system("cls");
			addproducts();
		}
		file.close();
	}
	void search()
	{
		int productid;
		char exit;
		cout << "Press 'e' & <enter> to exit or & other key to proceed & <enter>" << endl;
		cin >> exit;
		if (exit != 'e')
			{
			cout << "MilkID:0, RiceID:1, SugarID:2, ButterID:3, BreadID:4, MeatID:5, FishID:6, CerealID:7, CandyID:8\n";
			cout << "What product's information do you want to see? Enter it's ID here: ";
			cin >> productid;
			if (productid == 0)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[0] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[0] << "\n";
				cout << "UNIT PRRICE:" << price[0] << endl;

				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 1)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[1] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[1] << "\n";
				cout << "UNIT PRRICE:" << price[1] << endl;

				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 2)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[2] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[2] << "\n";
				cout << "UNIT PRRICE:" << price[2] << endl;
			}
			else if (productid == 3)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[3] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[3] << "\n";
				cout << "UNIT PRRICE:" << price[3] << endl;

				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}

			else if (productid == 4)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[4] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[4] << "\n";
				cout << "UNIT PRRICE:" << price[4] << endl;
				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 5)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[5] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[5] << "\n";
				cout << "UNIT PRRICE:" << price[5] << endl;
				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 6)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[6] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[6] << "\n";
				cout << "UNIT PRRICE:" << price[6] << endl;
				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 7)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[7] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[7] << "\n";
				cout << "UNIT PRRICE:" << price[7] << endl;
				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else if (productid == 8)
			{
				cout << "\t\tPRODUCT DETAILS\n";
				cout << "PRODUCT NAME:" << products[8] << "\n";
				cout << "TOTAL UNITS IN STOCK:" << subproductsnum[8] << "\n";
				cout << "UNIT PRRICE:" << price[8] << endl;
				cout << "Press 'e' & <enter> to go to stock or 's' & <enter> to search another items details";
				cin >> exit;

				if (exit == 'e')
				{
					stock();
				}
				else if (exit == 's')
				{
					system("cls");
					search();
				}
			}
			else
			{
				system("cls");
				search();
			}
		}
		else
		{
			stock();
		}
	}
