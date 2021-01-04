# Parla

//take a look please :D



#include <iostream>
    #include <ctime>
    using namespace std;

    void bubbleSort(int* DataBase, int size) { //this is the bubble sort, this one always keep on our program working
        int last, i;
        for (last = size - 1; last > 0; last--)// put in
        {
            //    DataBase[last] the largest element of DataBase[0..last];
            for (int i = 0; i < last; i++)
                if (*(DataBase + i + 1) < *(DataBase + i))
                {
                    int temp = DataBase[i + 1];
                    *(DataBase+ i + 1) = *(DataBase + i);
                    *(DataBase + i) = temp;
                }
        }
    }

    void NewClass(int* DataBase, int& size, int Newclass) //this is when we want to create a new class so:
    {
        bool Flag = true;
        for (int i = 0; i < size; i++)
        {
            if (*(DataBase + i) == Newclass) //we check if there is a Same class
            {
                Flag = false;
                break;
            }
        }
        if (Flag)
        {
            size++; //now we are make the new
            *(DataBase + size - 1) = Newclass;
            bubbleSort(DataBase, size);
        }
        for (int i = 0; i < size; i++) //and we just print them
        {    if (*(DataBase + i) != 0)
            cout << *(DataBase + i) << ' ';
            if (i == size - 1)
            {
                cout << endl;
            }
        }
    }

    void DelClass(int size, int* DataBase, int DelCode) //this is when we want to delete the Class
    {
        for (int i = 0; i < size; i++)
        {
            if (*(DataBase + i) == DelCode) //so we check any one of the classes, and after it delete them
            {
                *(DataBase + i) = DataBase[size - 1];
                DataBase[size - 1] = 0;
                size--;
                bubbleSort(DataBase, size); //and we want to fix the "Maharach"
            }
        }
    }
    int* SearchClass(int* DataBase, int size, int num) //now we are search with the Binary Search
    {
        bool binarySearch;
        int left = 0, right = size - 1, mid;
        while (left <= right) //this is the Binary Search
        {
            mid = (left + right) / 2;
            if (DataBase[mid] < num)
                left = mid + 1;
            else if (DataBase[mid] > num)
                right = mid - 1;
            else left = right + 1;
        }
        if (DataBase[mid] == num) 
        {
            int* Pointer = &(DataBase[mid]);
            return Pointer; //just to return
        }
        return NULL;
    }
    void PrintCode(int Code, int* DataBase, int size)  //this is easy one, we just do /1000 to the code
    {
        for (int i = 0; i < size; i++)
        {
            if (*(DataBase + i) / 1000 == Code) //and after it with any code in the DataBase we are check
            {
                cout << *(DataBase + i) << ' ';
            }

        }
        cout << endl;
    }

    void PrintAll(int size, int* DataBase) //and this is so easy, you just need to do 1 for
    {
        for (int i = 0; i < size; i++)
        {
            if (*(DataBase + i) != 0)
                cout << *(DataBase + i) << ' ';
        }
        cout << endl;
    }
    int main() //this is the main, the Main one
    { 

        cout << " Enter 0 to add a new classroom.\n";
        cout << "Enter 1 to delete a hybrid classroom.\n";
        cout << "Enter 2 to search for a specific classroom.\n";
        cout << "Enter 3 to print all the classsrooms for a specific Machon.\n";
        cout << "Enter 4 to print all the hybrid classrooms.\n";
        cout << "Enter 5 to exit.\n";
        cout << "Enter your choice:\n";
        enum Classes { add, delete1, search, printcode, printall, exit };
        int size = 0;
        int DataBase[50];
        int choice, Newclass, Delclass;
        cin >> choice;
        while (choice != 5)
        {
            switch (choice) //this is the switch
            {
            case add: //add func
                cout << "Enter the code of the classroom to add:\n";
                cin >> Newclass;
                while (Newclass < 10000 || Newclass > 99999)
                {
                    cout << "ERROR\n";
                    cin >> Newclass;
                }
                NewClass(DataBase, size, Newclass);
                break;
            case delete1: //delete func
                cout << "Enter the code of the classroom to delete:\n";
                int DelCode;
                cin >> DelCode;
                DelClass(size, DataBase, DelCode); 
                for (int i = 0; i < size; i++)
                {
                    if (*(DataBase + i) != 0)
                        cout << *(DataBase + i) << ' ';
                }
                cout << endl;
                break;
            case search: //search func
                cout << "Enter the code of the classroom to search for:\n";
                int num;
                cin >> num;
                if (SearchClass(DataBase, size, num))
                    cout << "Found\n";
                else
                    cout << "Not found\n";
                break;
            case printcode: //print code func
                cout << "Enter the code of the Machon:\n";
                int Code;
                cin >> Code;
                while (Code < 10 || Code > 99)
                {
                    cout << "ERROR\n";
                    cin >> Code;
                }
                PrintCode(Code, DataBase, size);
                break;
            case printall: //print all fun - the easy one
                PrintAll(size, DataBase);
            }
            cout << "Enter your next choice:\n"; //and if the user want to use it again this is agian he has other choice
            cin >> choice;
        }
        return 0;
        
      

        
        
        
        
        
        
