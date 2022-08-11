#include "stdafx.h"
#include <iostream>
using namespace std;
char matrix[3][3] = { '1','2','3','4','5','6','7','8','9' };
char joueur = 'X';
void PrintMatrix() {
	if (k == 0) {
		cout << "\ncette case est n'y pas vide .... trouve un autre case SPV !!!!!!!!!\n";
	system("cls");
	int i, j;
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			cout << matrix[i][j] << "  ";
		}
		cout << endl;
	}
}
void jouer() {
	char pos;
	int i, j,k=0;
	cout << "choiser votre position - joueur(" << joueur << "):";
	cin >> pos;
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			if (matrix[i][j] == pos) {
					matrix[i][j] = joueur;
					k = 1;
				}
			}
		}
	
	}
	if (k == 1) {
		if (joueur == 'X')
			joueur = 'O';
		else
			joueur = 'X';
	}
} 
char QuiGagné() {
	int x = 0, o = 0, c = 0,i,j;
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			if (matrix[i][j] != 'X' && matrix[i][j] != 'O') {
				c++;
			}
			if (matrix[i][j] == 'X') x++;
			else if (matrix[i][j] == 'O') o++;
			if (x == 3 || o == 3) {
				return x > o ? 'X' : 'O';
			}
		}
		x = 0; o = 0;
	}
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			if (matrix[j][i] == 'X') x++;
			else if(matrix[j][i] == 'O') o++;
			if (x == 3 || o == 3) {
				return x > o ? 'X' : 'O';
			}
		}
		x = 0; o = 0;
	}
	if (matrix[0][0] == 'X' && matrix[1][1] == 'X' && matrix[2][2] == 'X') return 'X';
	else if (matrix[0][0] == 'O' && matrix[1][1] == 'O' && matrix[2][2] == 'O') return 'O';
	else if (matrix[0][2] == 'X' && matrix[1][1] == 'X' && matrix[2][0] == 'X') return 'X';
	else if (matrix[0][2] == 'O' && matrix[1][1] == 'O' && matrix[2][0] == 'O') return 'O';
	if (c == 0) return 'Z';

	return '.';
}
int main()
{
	while (QuiGagné() == '.')
	{
		PrintMatrix();
		jouer();
	}
	PrintMatrix();
	if (QuiGagné() == 'Z')
		cout << "\n*************************************\nNULL !!!!!!\n*************************************\n";
	else
		cout << "\n*************************************\nbravo(" << QuiGagné() << ") Tu es Gagne\n*************************************\n";
		system("pause");
    return 0;
}

