# tictactoe
#Classic tictactoe game

from IPython.display import clear_output

def display_board(board):

    clear_output()
    print(board[1]+'|'+board[2]+'|'+board[3])
    print('-----')
    print(board[4]+'|'+board[5]+'|'+board[6])
    print('-----')
    print(board[7]+'|'+board[8]+'|'+board[9])

def player_input():
    
    choice = ''
    while choice != 'X' and choice != 'O':
        choice = input('Player 1: Choose X or O: ').upper()
        
    if choice == 'X':
        return ('X','O')
    else:
        return ('O','X')

def place_marker(board, marker, position):
    
    board[position]=marker

def win_check(board, mark):
    
    return ((board[1]==board[2]==board[3]==mark) or
            (board[4]==board[5]==board[6]==mark) or
            (board[7]==board[8]==board[9]==mark) or
            (board[1]==board[4]==board[7]==mark) or
            (board[2]==board[5]==board[8]==mark) or
            (board[3]==board[6]==board[9]==mark) or
            (board[1]==board[5]==board[9]==mark) or
            (board[3]==board[5]==board[7]==mark))

import random

def choose_first():
    first = random.randint(0,1)
    if first == 0:
        return 'Player 1'
    else:
        return 'Player 2'

def space_check(board, position):
    
    return board[position]==' '

def full_board_check(board):
    
    for val in range(1,9):
        if space_check(board, val):
            return False
    return True

def player_choice(board):
    
    position = 0
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
        position = int(input("Enter a position: "))
        
    return position

def replay():
    
    choice = input("Do you want to play again?(Y or N): ").upper()
    return choice == 'Y'

print('Welcome to Tic Tac Toe!')

while True:
    # Set the game up here
    board = [' ']*10
    player1choice, player2choice = player_input()
    
    turn = choose_first()
    print(turn + ' will go first')
    
    #pass
    
    game_on = True

    while game_on:
        #Player 1 Turn
        if turn == 'Player 1':
            display_board(board)
            position=player_choice(board)
            place_marker(board,player1choice,position)
            
            if win_check(board,player1choice):
                display_board(board)
                print('Congratulations! Player 1 just won')
                game_on = False
                
            elif full_board_check(board):
                print('Game Tied')
                game_on = False
                
            else:
                turn = 'Player 2'
        
        # Player2's turn.
        else:
            display_board(board)
            position=player_choice(board)
            place_marker(board,player2choice,position)
            
            if win_check(board,player2choice):
                display_board(board)
                print('Congratulations! Player 2 just won')
                game_on = False
                
            elif full_board_check(board):
                display_board(board)
                print('Game Tied')
                game_on = False
                
            else:
                turn = 'Player 1'
        
            #pass
    if not replay():
        break    
