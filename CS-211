#include <iostream>
#include <iomanip>
#include <ctime>
#include <cstdlib>
#include <fstream>

using namespace std;

int main()
{
	ofstream outFile;

	outFile.open("Neutron Statistics.txt");

	float neutron, dir_change_tot, motions_tot, escaped;
	int forward, right, motions, dir_change;
	int shield, neutron_max, dir_max;
	int direction, prev_dir;
	
	neutron = 1;
	forward = right = motions = motions_tot = dir_change = dir_change_tot = prev_dir = escaped = 0;

	float esc_percent, dir_change_avg, motions_avg;

	srand(time(0));

	cout << "Enter Shield Thickness: ";
	cin >> shield;

	cout << "Enter Number of Neutrons in Generator: ";
	cin >> neutron_max;
	
	cout << "Enter Max Number of Neutron Direction Changes: ";
	cin >> dir_max;

	cout << "\n";

	outFile << setw(15) << "Neutron ID" << setw(25) << "Direction Changes" << setw(25) << "Random Motions" << setw(25) << "Final Status" << endl;
	outFile << setw(15) << "==========" << setw(25) << "=================" << setw(25) << "==============" << setw(25) << "============" << endl;

	while (neutron <= neutron_max) {
		direction = (rand() % 4) + 1;

		prev_dir = 0;
		motions += 1;
		motions_tot += 1;

		if (direction != prev_dir && motions > 1) {
			dir_change += 1;
			dir_change_tot += 1;
		}

		if (direction == 1) {
			forward += 1;

			prev_dir = 1;

			cout << "A forward motion has occurred." << endl;
		}

		else if (direction == 2) {
			forward -= 1;

			prev_dir = 2;

			cout << "A backward motion has occurred." << endl;
		}

		else if (direction == 3) {
			right -= 1;

			prev_dir = 3;

			cout << "A lateral left motion has occurred." << endl;
		}

		else if (direction == 4) {
			right += 1;

			prev_dir = 4;

			cout << "A lateral right motion has occurred." << endl;
		}

		if (forward > shield) {
			escaped += 1;

			outFile << setw(15) << neutron << setw(25) << dir_change << setw(25) << motions << setw(25) << "Escaped" << endl;

			neutron += 1;
			forward = right = motions = dir_change = 0;

			if (neutron <= neutron_max) {
				cout << "Neutron has escaped. A new neutron is now being tracked..." << endl;
			}

			else {
				cout << "Neutron has escaped. All neutrons have been accounted for.\n\n" << endl;
			}
		}

		if (dir_change > dir_max && forward <= shield) {

			outFile << setw(15) << neutron << setw(25) << dir_change << setw(25) << motions << setw(25) << "Destroyed" << endl;

			neutron += 1;
			forward = right = motions = dir_change = 0;

			if (neutron <= neutron_max) {
				cout << "Neutron has been destroyed. A new neutron is now being tracked..." << endl;
			}

			else {
				cout << "Neutron has been destroyed. All neutrons have been accounted for.\n\n" << endl;
			}
		}
	}

	esc_percent = (escaped / neutron) * 100;
	dir_change_avg = dir_change_tot / neutron;
	motions_avg = motions_tot / neutron;

	outFile << "\n\n\tEscaped Neutrons: " << escaped << endl;
	outFile << "\tPercentage of Escaped: " << esc_percent << "%" << endl;
	outFile << "\tTotal Direction Changes: " << dir_change_tot << endl;
	outFile << "\tAverage Direction Changes: " << dir_change_avg << endl;
	outFile << "\tTotal Random Motions: " << motions_tot << endl;
	outFile << "\tAverage Random Motions: " << motions_avg << endl;

	outFile.close();

	system("pause");
	return 0;
}
