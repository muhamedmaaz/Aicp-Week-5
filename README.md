# Aicp-Week-5
#include<iostream>
using namespace std;

char board[3][3] = {{'1', '2', '3'}, {'4', '5', '6'}, {'7', '8','9'}};

int choice;
int row, column;
char turn = 'X';
bool draw = false;

void display_board()
{
	cout<<"\n\tPlayer - 1 [X] \t Player - 2 [O]\n\n";
	cout<<"\t     |     |     "<<endl;
	cout<<"\t  "<<board[0][0]<<"  | "<<board[0][1]<<"   | "<<board[0][2]<<endl;
	cout<<"\t_____|_____|_____"<<endl;
	cout<<"\t     |     |     "<<endl;
	cout<<"\t  "<<board[1][0]<<"  | "<<board[1][1]<<"   | "<<board[1][2]<<endl;
	cout<<"\t_____|_____|_____"<<endl;
	cout<<"\t     |     |     "<<endl;
	cout<<"\t  "<<board[2][0]<<"  | "<<board[2][1]<<"   | "<<board[2][2]<<endl;
	cout<<"\t     |     |     "<<endl;
}

void player_turn()
{
	if(turn == 'X')
		cout<<"\n\tPlayer - 1 [X] turn:";
	else if(turn == 'O')
		cout<<"\n\tPlayer - 2 [O] turn:";
	
	cin>>choice;
	
	switch(choice)
	{
		case 1: row=0; column=0; break;
		case 2: row=0; column=1; break;
		case 3: row=0; column=2; break;
		case 4: row=1; column=0; break;
		case 5: row=1; column=1; break;
		case 6: row=1; column=2; break;
		case 7: row=2; column=0; break;
		case 8: row=2; column=1; break;
		case 9: row=2; column=2; break;
		
		default:
			cout<<"Invalid Position"<<endl;
			player_turn();
	
	}
	if(turn == 'X' && board[row][column] != 'X' && board[row][column] != 'O'){
		board[row][column] = 'X';
		turn = 'O';
	}
	else if(turn == 'O' && board[row][column] != 'X' && board[row][column] != 'O'){
		board[row][column] = 'O';
		turn = 'X';
	}
	else{
		cout<<"Position already filled!\nChoose another position"<<endl;
		player_turn();
	}
	display_board();
}

bool gameover()
{
	for(int i=0;i<3;i++)
		if(board[i][0] == board[i][1] && board[i][0] == board[i][2] || board[0][i] == board[1][i] && board[0][i] == board[2][i] )
			return false;
	if(board[0][0] == board[1][1] && board[0][0] == board[2][2] || board[0][2] == board[1][1] && board[0][2] == board[2][0] )
		return false;
		
	for(int i=0; i<3;i++)
		for(int j=0;j<3;j++)
			if(board[i][j] !='X' && board[i][j] !='O')
				return true;
	
	draw = true;
	return false;
}

int main()
{
	cout<<"\t\t\tTick-Tac-Toe\t\t\t"<<endl;
	cout<<"\t\t\tFor 2 Players\t\t\t"<<endl;
	while(gameover()){
		display_board();
		player_turn();
	}
	if(turn == 'X' && draw == false)
		cout<<"\n\nPlayer 2 [O] has won the game"<<endl;
	else if(turn == 'O' && draw == false)
		cout<<"\n\nPlayer 1 [X] has won the game"<<endl;
	else
		cout<<"\n\nGame Over!\n\n";
		
	return 0;
}

