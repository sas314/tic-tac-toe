# tic-tac-toe
import tkinter as tk
from tkinter import *
def new_game():
    label.config(text=players[0] + " turn", fg='#000')
    for r in range(3):
        for c in range(3):
            buttons[r][c] = Button(frame, text="", font=("Helvetica", 20), width=5, height=2,
                                   command=lambda row=r, column=c: next_turn(row, column))
            buttons[r][c].grid(row=r, column=c, padx=5, pady=5)
def next_turn(row, column):
    global player
    if buttons[row][column]['text'] == "" and not check_win():
        buttons[row][column]['text'] = player
    if (player == players[0]):
        buttons[row][column]['fg'] = '#f80'
    if (player == players[1]):
            buttons[row][column]['fg'] = '#0f0'
    if not check_win():
            if (player == players[0]):
               player = players[1]
               label.config(text=players[1] + " turn")
            else:
                player = players[0]
                buttons[row][column]['fg']='#0f0'

                label.config(text=players[0] + " turn")
    else:
            label.config(text=player + " is  win ",fg='#f00')
def check_win():
    # Check rows for a win
    for row in range(3):
        if buttons[row][0]['text'] == buttons[row][1]['text'] == buttons[row][2]['text'] != "":
            return True
    # Check columns for a win
    for col in range(3):
        if buttons[0][col]['text'] == buttons[1][col]['text'] == buttons[2][col]['text'] != "":
            return True
    # Check diagonals for a win
    if buttons[0][0]['text'] == buttons[1][1]['text'] == buttons[2][2]['text'] != "":
        return True
    if buttons[0][2]['text'] == buttons[1][1]['text'] == buttons[2][0]['text'] != "":
        return True
    return False
players = ["X", "O"]
player = players[0]
window = tk.Tk()
buttons = [[0, 0, 0],
           [0, 0, 0],
           [0, 0, 0]]
label = tk.Label(text=player + " turn", font=("Helvetica", 30, "bold"))
label.pack()
buttons_new_game = Button(window, text="New Game", font=("Helvetica", 15, "bold"), command=new_game)
buttons_new_game.pack()
frame = Frame(window)
frame.pack()
for r in range(3):
    for c in range(3):
        buttons[r][c] = Button(frame, text="", font=("Helvetica", 20), width=5, height=2, command=lambda row=r, column=c: next_turn(row, column))
        buttons[r][c].grid(row=r, column=c, padx=5, pady=5)
window.mainloop()
