# Disk-Scheduling-Policies

A program that does a Monte Carlo simulation of four disk scheduling algorithms: 1. First-In-First-Out (FIFO), 2. Shortest-Service-Time-First (SSTF), 3. SCAN, and 4. Circular SCAN (C-SCAN). The program runs 100 simulations for each number of I/O requests (5 - 50 inclusive). It randomly generates a sequence of unique track numbers from 1 – 199 (inclusive) in each simulation of each number of I/O requests and then computes the average seek time over the 100 simulations of each number of I/O requests for each algorithm.

The four disk scheduling algorithms are described as follows:

**FIFO:** FIFO processes items from the queue in sequential order, i.e. the requests are processed in the order received.

**SSTF:** SSTF selects the disk I/O request that requires the least movement of the disk arm from its current position, i.e. it chooses to process the item that will give the minimum seek time.

**SCAN:** With SCAN, the disk arm is required to move in one direction only, satisfying all outstanding requests en route, until it reaches the last track in that direction or until there are no more requests in that direction. The service direction is then reversed and the scan proceeds in the opposite direction, again picking up all requests in order.

**C-SCAN:** The C-SCAN policy restricts scanning to one direction only. Thus, when the last track has been visited in one direction, the arm is returned to the opposite end of the disk and the scan begins again in the same direction.

### Program Description:

A function named “generateRandomNum” generates a random track number for an I/O request. It returns a random integer between 1 - 199 (inclusive).

A global array of integers, trackNums, holds the sequence of track numbers randomly generated by generateRandomNum(). A global array of doubles, seekArray, holds the average seek time of each algorithm for each number of I/O requests.

A function named “FIFO” fulfills a given number of I/O requests using the FIFO algorithm. The function starts by assigning the current track number to be 100. It then loops from 0 to the number of I/O requests to go through in trackNums. While looping, it accumulates the seek times and assigns the current track number to be the next track number in trackNums. Seek time is calculated by computing the absolute difference between the current track number and the next track number in trackNums. After going through all the required tracks, it divides the total seek time by the number of I/O requests to get the average seek time and stores the result in seekArray.

A function named “SSTF” fulfills a given number of I/O requests using the SSTF algorithm. The function starts by assigning the current track number to be 100. It then loops from 0 to the number of I/O requests to go through in trackNums. While looping, it goes through trackNums to find the track number that will produce the shortest seek time. Once that track number is found, it adds the shortest seek time to the total seek time and selects that track number to be the next track number. Seek time is calculated by computing the absolute difference between the current track number and the next track number. After exiting the loop, it divides the total seek time by the number of I/O requests to get the average seek time and stores the result in seekArray.

A function named “SCAN” fulfills a given number of I/O requests using the SCAN algorithm. The function assigns the current track number to be 100. It first sorts the sequence of track numbers in ascending order in a temporary array, and then loops through the array to find the position of the starting track number (100) in the array. It then loops through all the track numbers greater than the starting track number in ascending order beginning from the starting track number and ending at the largest track number. This is done to go through all the tracks in the forward direction. Once the last track in the forward direction is visited, it reverses its direction by looping through all the track numbers smaller than the starting track number in descending order beginning from the starting track number and ending at the smallest track number. While looping through the track numbers, both greater and smaller than the starting track number, it accumulates the seek times and assigns the current track number to be the next track number in the loop. Seek time is calculated by computing the absolute difference between the current track number and the next track number. After going through all the tracks, it divides the total seek time by the number of IO requests to get the average seek time and stores the result in seekArray.

A function named “CSCAN” fulfills a given number of I/O requests using the C-SCAN algorithm. The function assigns the current track number to be 100. It first sorts the sequence of track numbers in ascending order in a temporary array, and then loops through the array to find the position of the starting track number (100) in the array. It then loops through all the track numbers greater than the starting track number in ascending order beginning from the starting track number and ending at the largest track number. This is done to go through all the tracks in the forward direction. Once the last track in the forward direction is visited, it jumps to the opposite end of the disk, i.e. to the shortest track number, and starts the scan in the forward direction from there. This is done by looping through all the track numbers smaller than the starting track number in ascending order beginning from the smallest track number and ending at the starting track number. While looping through the track numbers, both greater and smaller than the starting track number, it accumulates the seek times and assigns the current track number to be the next track number in the loop. Seek time is calculated by computing the absolute difference between the current track number and the next track number. After going through all the tracks, it divides the total seek time by the number of I/O requests to get the average seek time and stores the result in seekArray.

The main function starts by looping through the numbers of I/O requests, beginning at 5 and ending at 50. Within that loop, another loop is created which runs from 0 to 100 to run 100 simulations for each number of I/O requests. Within the simulation loop, a sequence of track numbers is generated by calling generateRandomNum(). A while loop is used to ensure that each random number generated is unique. This is done by first creating an array of 200 elements, randomNumbersArray. Each element has a value of either 0 or 1, with 0 indicating that the corresponding index number has not been used as a track number and 1 indicating that the corresponding index number has been used as a track number. For instance, if randomNumbersArray[34] is equal to 1, it means that the number 34 has already been used as a track number, so a different random number has to be used. The while loop keeps looping until a random number such that randomNumbersArray[random number] == 0 is found. Once such a number is found, the program assigns 1 to that element of the array to indicate that it is in use and breaks from the while loop. Once a sequence of unique random numbers has been created, the function calls FIFO(), SSTF(), SCAN() and CSCAN() with the number of I/O requests as the argument to the functions to compute the average seek times. After the average seek times are calculated, the function displays a table consisting of the average seek time of each algorithm for each number of I/O requests to the console by looping through seekArray. While looping, it also writes the table to a text file which can be used for further analysis of the algorithms.

### Building and running the program:

1. In the working directory, where the program source code is saved, enter the following command to build the code:

        gcc program5.c -o program5

   where program5. is the program source code and program5 is the executable.

2. Enter the following command to run the program:

        ./program5
