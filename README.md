# campus-room-allocation-system
A room allocation system is a software solution designed to efficiently assign rooms based on user needs, availability, and predefined criteria. It helps manage bookings, avoid conflicts, optimize space usage, and streamline operations in environments like hostels, hotels, offices, or universities.
#include <iostream>
using namespace std;

/* ================= PART 1 : INPUT ================= */

void inputRooms(int status[], int n)
{
    cout << "\nEnter room status (1 = Occupied, 0 = Empty):\n";
    for (int i = 0; i < n; i++)
    {
        cout << "Room " << i + 1 << " : ";
        cin >> status[i];
    }
}

/* ================= PART 2 : LINEAR SEARCH ================= */

int linearSearch(int status[], int n)
{
    for (int i = 0; i < n; i++)
    {
        if (status[i] == 0)
            return i;
    }
    return -1;
}

/* ================= PART 3 : SORTING ================= */

void sortRooms(int status[], int roomNo[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (status[j] > status[j + 1])
            {
                int temp = status[j];
                status[j] = status[j + 1];
                status[j + 1] = temp;

                int temp2 = roomNo[j];
                roomNo[j] = roomNo[j + 1];
                roomNo[j + 1] = temp2;
            }
        }
    }
}

/* ================= PART 4 : BINARY SEARCH ================= */

int binarySearch(int status[], int roomNo[], int n)
{
    int low = 0, high = n - 1;
    int answer = -1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (status[mid] == 0)
        {
            answer = roomNo[mid];   // actual room number
            high = mid - 1;
        }
        else
        {
            low = mid + 1;
        }
    }

    return answer;
}

/* ================= DISPLAY ================= */

void displayRooms(int status[], int roomNo[], int n)
{
    cout << "\nRoom Status:\n";

    for (int i = 0; i < n; i++)
    {
        if (status[i] == 0)
            cout << "Room " << roomNo[i] << " is Empty\n";
        else
            cout << "Room " << roomNo[i] << " is Occupied\n";
    }
}

/* ================= MAIN ================= */

int main()
{
    int n;
    cout << "Enter total number of rooms: ";
    cin >> n;

    int status[100];
    int roomNo[100];

    for (int i = 0; i < n; i++)
        roomNo[i] = i + 1;

    // INPUT
    inputRooms(status, n);

    // LINEAR SEARCH (original data)
    int first = linearSearch(status, n);

    if (first != -1)
        cout << "\nFirst empty room is at Room " << first + 1 << endl;
    else
        cout << "\nNo empty room found\n";

    // SORTING
    sortRooms(status, roomNo, n);

    // BINARY SEARCH 
    int check = binarySearch(status, roomNo, n);

    // FINAL DISPLAY
    displayRooms(status, roomNo, n);

    return 0;
}
