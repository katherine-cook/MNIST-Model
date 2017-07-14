#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Fri Jul  7 15:38:25 2017

@author: KatherineCook
"""

#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Mar 15 11:03:53 2017

@author: KatherineCook
"""
import tkinter as tk
import random

root=tk.Tk()
root.title("2048")
class Gui():
    rows=4
    columns=4
    num_arr=[[0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0]]
    def __init__(self,root):
        self.root=root
        self.canvas=tk.Canvas(root, width=600, height=600, background='#f0ffff')
        self.canvas.grid(row=2,column=0)
        self.root.grid_columnconfigure(0,weight=1)
        
#        self.frame = tk.Frame(self.root)
#        self.frame.grid(row=0,column=0,sticky='nsew')
        self.create_grid()
        self.change_color()
        
    def create_grid(self):
        self.grid = [[self.canvas.create_rectangle(100*j+100, 100*i+100, 100*(j+1)+100, 100*(i+1)+100, width=10,outline="#cdb79e",fill="#cdc0b0") for j in range(4)] for i in range(4)]
        self.text_grid = [[self.canvas.create_text(100*j + 150, 100*i+150, font=("Helvetica", 25),text="") for j in range(4)] for i in range(4)]
        self.header = self.canvas.create_text(300, 55, font=("Courier", 70,"bold"),text="2048", fill="#ff7f50")
        self.instructions = self.canvas.create_text(305, 87, font=("Courier", 12),text="Move arrow keys up, down, left and right to move tiles")
        self.insert_rand_int() #calls rand_int twice to generate two 2's
        self.insert_rand_int()
    def create_blank_grid(self):
        self.blank = [[self.canvas.create_rectangle(100*j+100, 100*i+100, 100*(j+1)+100, 100*(i+1)+100, width=10,outline="#cdb79e",fill="#cdc0b0") for j in range(4)] for i in range(4)]
        self.header = self.canvas.create_text(300, 55, font=("Courier", 70,"bold"),text="2048", fill="#ff7f50")
       
    def is_last_move(self):
        spots_avail = 0 
        for i in range(self.rows):
            for j in range(self.columns):
                if self.num_arr[i][j] ==0:
                    spots_avail = spots_avail+1
                    last_avail_i = i 
                    last_avail_j = j
                    return False
        if spots_avail == 1:
            self.num_arr[last_avail_i][last_avail_j]=2
            return False
        elif spots_avail ==0:
            self.game_over()
            return True
    
    def insert_rand_int(self): 
        self.is_last_move()
        rand_j = random.randint(0,3)
        rand_i = random.randint(0,3)
        while self.num_arr[rand_i][rand_j]!=0:
            #can't put a two here, regenerate a random position 
            rand_j = random.randint(0,3)
            rand_i = random.randint(0,3)
        self.num_arr[rand_i][rand_j]=2
        self.change_color() #update background and text of random two tiles
        #self.print_num_arr()
            
    def change_color(self):   #update UI when numbers are merged, win game if get to 2048     
        for i in range(self.rows):
            for j in range(self.columns):
                #print(self.num_arr[i][j])               
                if self.num_arr[i][j]!=0:
                    num_text=str(self.num_arr[i][j])
                    self.canvas.itemconfigure(self.text_grid[i][j],text=num_text)#reconfigure text from create.text
                if self.num_arr[i][j]==0:
                    self.canvas.itemconfigure(self.text_grid[i][j],text="")
                    self.canvas.itemconfig(self.grid[i][j],fill="#cdc0b0") 
                if self.num_arr[i][j]==2:
                    self.canvas.itemconfig(self.grid[i][j],fill="#faebd7") 
                elif self.num_arr[i][j]== 4:
                    self.canvas.itemconfig(self.grid[i][j],fill="#f5deb3")
                elif self.num_arr[i][j]== 8:
                    self.canvas.itemconfig(self.grid[i][j],fill="#f4a460")
                elif self.num_arr[i][j]== 16:
                    self.canvas.itemconfig(self.grid[i][j],fill="#ffa500")
                elif self.num_arr[i][j]== 32:
                    self.canvas.itemconfig(self.grid[i][j],fill="#ff7f50")
                elif self.num_arr[i][j]== 64:
                    self.canvas.itemconfig(self.grid[i][j],fill="#ff6347")  
                elif self.num_arr[i][j]== 128:
                    self.canvas.itemconfig(self.grid[i][j],fill="#FFD700")
                elif self.num_arr[i][j]== 256:
                    self.canvas.itemconfig(self.grid[i][j],fill="#FFAFA7")
                elif self.num_arr[i][j]== 512:
                    self.canvas.itemconfig(self.grid[i][j],fill="#D5F278")
                elif self.num_arr[i][j]== 1024:
                    self.canvas.itemconfig(self.grid[i][j],fill="#eedd82")  
                elif self.num_arr[i][j]== 2048:
                    self.canvas.itemconfig(self.grid[i][j],fill="#ffff00")
                    self.congrats() #congradulatory message if won

    '''try_move(i,j,dir, row_by_row, merged) tries to move a single tile located at position i,j in the direction dir. '''
    def try_move(self,i,j,str_dir,row_by_row,merged):#returns bool for merged         
        if str_dir=="right": #case for rightKey 
            for k in range(j+1,4):
                if self.num_arr[i][j]==self.num_arr[i][k] and merged==False: #can merge two tiles 
                    added_val = self.num_arr[i][j] + self.num_arr[i][k]
                    self.num_arr[i][k]=added_val
                    self.num_arr[i][j]=0 #Update num_arr
                    return True
                elif self.num_arr[i][k]==0: #blank spaces to move 
                    if k==3: #at edge of board
                        self.num_arr[i][k]=self.num_arr[i][j]
                        self.num_arr[i][j]=0 #Update num_arr
                        return False #didn't merge
                else:                                
                    #j and k are not equal
                    temp = self.num_arr[i][j] #collision with non-similar tile number 
                    self.num_arr[i][j]=0 #if the number was shifted to the right, make its old spot=0
                    self.num_arr[i][k-1]=temp #if it didn't move at all, keep it where it is
                    return False #doesn't merge tiles

        elif str_dir=="left": #case for leftKey 
            for k in range(j-1,-1,-1):              
                if self.num_arr[i][j]==self.num_arr[i][k] and merged==False: #can merge two tiles 
                    added_val = self.num_arr[i][j] + self.num_arr[i][k]
                    self.num_arr[i][k]=added_val
                    self.num_arr[i][j]=0 #added val moves to position k 
                    return True
                elif self.num_arr[i][k]==0: #blank spaces to move 
                    if k==0: #at edge of board
                        self.num_arr[i][k]=self.num_arr[i][j]
                        self.num_arr[i][j]=0 #Update num_arr
                        return False #didn't merge
                else:                                
                    #j and k are not equal
                    temp = self.num_arr[i][j] #collision with non-similar tile number 
                    self.num_arr[i][j]=0 #if the number was shifted to the left, make its old spot=0
                    self.num_arr[i][k+1]=temp #if it didn't move at all, keep it where it is
                    return False #doesn't merge tiles 

        elif str_dir=="up": #case for upKey 
            for k in range(i-1,-1,-1): 
                if self.num_arr[i][j]==self.num_arr[k][j] and merged==False: #can merge two tiles 
                    added_val = self.num_arr[i][j] + self.num_arr[k][j]
                    self.num_arr[k][j]=added_val
                    self.num_arr[i][j]=0 #Update num_arr
                    return True
                elif self.num_arr[k][j]==0: #blank spaces to move
                    if k==0: #at edge of board
                        self.num_arr[k][j]=self.num_arr[i][j]
                        self.num_arr[i][j]=0 #Update num_arr
                        return False #didn't merge                        
                else:                                
                    #j and k are not equal
                    temp = self.num_arr[i][j] #collision with non-similar tile number 
                    self.num_arr[i][j]=0 #if the number was shifted to the right, make its old spot=0
                    self.num_arr[k+1][j]=temp #if it didn't move at all, keep it where it is
                    return False #doesn't merge tiles
                        
        elif str_dir=="down": #case for downKey 
            for k in range(i+1,4): 
                if self.num_arr[i][j]==self.num_arr[k][j] and merged==False: #can merge two tiles 
                    added_val = self.num_arr[i][j] + self.num_arr[k][j]
                    self.num_arr[k][j]=added_val
                    self.num_arr[i][j]=0 #Update num_arr
                    return True
                elif self.num_arr[k][j]==0: #blank spaces to move
                    if k==3: #at edge of board
                        self.num_arr[k][j]=self.num_arr[i][j]
                        self.num_arr[i][j]=0 #Update num_arr
                        return False #didn't merge
                else:                                
                    #j and k are not equal
                    temp = self.num_arr[i][j] #collision with non-similar tile number 
                    self.num_arr[i][j]=0 #if the number was shifted to the right, make its old spot=0
                    self.num_arr[k-1][j]=temp #if it didn't move at all, keep it where it is
                    return False #doesn't merge tiles
                
    '''iterate_grid(dir,row_by_row) steps through the entire grid. It starts in the first index of 
    dir and progresses either column by column or row by row depending on the boolean value of row by row. it 
    checks if there is a number at each position i,j. If yes, it will call try_move 
    for that position'''
    def iterate_grid(self,index_order,row_by_row,str_dir):        
        if row_by_row==True:
            for i in range(self.rows):
                merged=False
                for j in index_order:
                    if self.num_arr[i][j]!=0:
                        if self.try_move(i,j,str_dir,row_by_row,merged)==True: 
                            #if it gets here, there was a merge
                            #try_move returns a bool
                            merged=True
        else:
            for j in range(self.columns): #j is column number
                merged=False
                for i in index_order:
                    if self.num_arr[i][j]!=0:                        
                        if self.try_move(i,j,str_dir,row_by_row,merged)==True:
                            merged=True
        #self.print_num_arr()
        self.change_color() #update UI 
        
        
    def rightKey(self,event): #gets click of right arrow button 
        #print("Right")
        index_order=[3,2,1,0] #col numbers for right direction 
        str_dir ="right"
        row_by_row=True #right and left iterate through columns first 
        self.iterate_grid(index_order,row_by_row,str_dir)
        self.insert_rand_int()
        
    def leftKey(self,event):#gets click of left arrow button 
        #print("Left")
        index_order=[0,1,2,3] #col numbers 
        str_dir ="left"
        row_by_row=True
        self.iterate_grid(index_order, row_by_row,str_dir)
        self.insert_rand_int()
        
    def upKey(self,event):#gets click of up arrow button 
        #print("Up")
        index_order=[0,1,2,3] #row numbers
        str_dir ="up"
        row_by_row=False #up and down iterate down each row
        self.iterate_grid(index_order,row_by_row,str_dir)  #iterate column by column 
        self.insert_rand_int()
        
    def downKey(self,event):#gets click of down arrow button 
        #print("Down")
        index_order=[3,2,1,0] #row numbers 
        str_dir ="down"
        row_by_row=False #up and down iterate down(or up) each row  
        self.iterate_grid(index_order,row_by_row,str_dir) #iterate column by column
        self.insert_rand_int()
        
#    def print_num_arr(self):
#        print() #to check numbers in num_arr in console
#        for i in range(4):
#            print(self.num_arr[i])

    def game_over(self):
        self.gameover = self.canvas.create_text(300, 300, font=("Courier", 40),text="GAME OVER")
        self.messagebox.showwarning("Game Over","Game Over!")
        
    def congrats(self):
        self.instructions = self.canvas.create_text(300, 300, font=("Courier", 50),text="YOU WIN!")
        self.tk.messagebox.showinfo("Congrats!", "You Got to 2048!")
        self.create_blank_grid()                

grid=Gui(root)

root.bind("<Left>", grid.leftKey)
root.bind('<Right>', grid.rightKey)
root.bind('<Up>', grid.upKey)
root.bind('<Down>', grid.downKey)
root.mainloop()