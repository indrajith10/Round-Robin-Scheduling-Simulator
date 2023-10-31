#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Define the process structure
typedef struct {
    int process_id;
    int arrival_time;
    int burst_time;
    int remaining_time;
    int waiting_time;
    int turnaround_time;
} Process;

int main() {
    int num_processes = 10;
    int time_quantum = 2;
    int total_time_units = 100;

    // Seed the random number generator
    srand(time(NULL));

    // Create an array to store the processes
    Process processes[num_processes];

    // Initialize processes with random arrival times and burst times
    for (int i = 0; i < num_processes; i++) {
        processes[i].process_id = i + 1;
        processes[i].arrival_time = rand() % 21; // Random arrival time between 0 and 20
        processes[i].burst_time = (rand() % 10) + 1; // Random burst time between 1 and 10
        processes[i].remaining_time = processes[i].burst_time;
        processes[i].waiting_time = 0;
        processes[i].turnaround_time = 0;
    }

    int current_time = 0;
    int completed_processes = 0;

    while (current_time < total_time_units && completed_processes < num_processes) {
        for (int i = 0; i < num_processes; i++) {
            if (processes[i].remaining_time > 0) {
                if (processes[i].remaining_time > time_quantum) {
                    // Process runs for a time quantum
                    current_time += time_quantum;
                    processes[i].remaining_time -= time_quantum;
                } else {
                    // Process completes
                    current_time += processes[i].remaining_time;
                    processes[i].waiting_time += current_time - processes[i].arrival_time - processes[i].burst_time;
                    processes[i].remaining_time = 0;
                    completed_processes++;
                }
            }
        }
    }

    // Calculate turnaround time based on waiting time and burst time
    for (int i = 0; i < num_processes; i++) {
        processes[i].turnaround_time = processes[i].waiting_time + processes[i].burst_time;
    }

    // Calculate and display the average waiting time and turnaround time
    float total_waiting_time = 0, total_turnaround_time = 0;
    for (int i = 0; i < num_processes; i++) {
        total_waiting_time += processes[i].waiting_time;
        total_turnaround_time += processes[i].turnaround_time;
    }

    float avg_waiting_time = total_waiting_time / num_processes;
    float avg_turnaround_time = total_turnaround_time / num_processes;

    printf("Average Waiting Time: %.2f\n", avg_waiting_time);
    printf("Average Turnaround Time: %.2f\n", avg_turnaround_time);

    // Calculate the ideal scenario results
    // In an ideal scenario, all processes are scheduled with no waiting time.
    float ideal_avg_waiting_time = 0;

    // Calculate the ideal scenario turnaround time
    // In an ideal scenario, turnaround time is the same as burst time.
    float ideal_avg_turnaround_time = 0;
    for (int i = 0; i < num_processes; i++) {
        ideal_avg_turnaround_time += processes[i].burst_time;
    }

    ideal_avg_turnaround_time /= num_processes;

    printf("Ideal Average Waiting Time: %.2f\n", ideal_avg_waiting_time);
    printf("Ideal Average Turnaround Time: %.2f\n", ideal_avg_turnaround_time);

    // Compare the results
    float waiting_time_difference = avg_waiting_time - ideal_avg_waiting_time;
    float turnaround_time_difference = avg_turnaround_time - ideal_avg_turnaround_time;

    if (waiting_time_difference > 0) {
        printf("The scheduler resulted in an increased waiting time by %.2f units.\n", waiting_time_difference);
    } else if (waiting_time_difference < 0) {
        printf("The scheduler improved waiting time by %.2f units in the ideal scenario.\n", -waiting_time_difference);
    } else {
        printf("The waiting time remains the same as in the ideal scenario.\n");
    }

    if (turnaround_time_difference > 0) {
        printf("The scheduler resulted in an increased turnaround time by %.2f units.\n", turnaround_time_difference);
    } else if (turnaround_time_difference < 0) {
        printf("The scheduler improved turnaround time by %.2f units in the ideal scenario.\n", -turnaround_time_difference);
    } else {
        printf("The turnaround time remains the same as in the ideal scenario.\n");
    }

    return 0;
}
