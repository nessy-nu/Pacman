import re
class pacman:
    """
    
    """
    def __init__(self):
        """
        Constructor method 
        """
        self.position =[]
        self.facing = ""
    
    def place(self,x,y,f):
        """ 
        Places the Pacman on the board  
  
        Parameters: 
        x (int): Position of the Pacman on the x-axis
        y (int): Position of the Pacman on the y-axis
        f (string): Direction of the Pacman
        
        Returns: 
        Print Statement: Feedback to user whether Pacman was placed on board or not 
  
        """
        self.position = [x,y]
        self.facing = f
        print("Valid placing, the position of your Pacman is: {},{},{}". format(self.position[0],self.position[1], self.facing))
    
    def move(self,valid_move):
        """ 
        Moves the Pacman on the map one unit  
  
        Parameters: 
        valid_move (boolean): Indicates if Pacman can move without it falling off the board
        
  
        """
        [x,y] = self.get_position()
        if valid_move:
            if self.facing == "NORTH":
                self.position = [x,y+1] 
            elif self.facing == "SOUTH":
                self.position = [x,y-1] 
            elif self.facing == "EAST":
                self.position = [x+1,y] 
            elif self.facing == "WEST":
                self.position = [x-1,y] 
        else:
            self.position = [x,y]
            
    def check(self):
        """ 
        Checks that the requested move for Pacman won't move him off the board  
        
        Returns: 
        Boolean: Valid move or not
  
        """
        [x,y] = self.get_position()
        if self.facing =="NORTH":
            y+=1
        elif self.facing =="SOUTH":
            y-=1
        elif self.facing =="EAST":
            x+=1
        elif self.facing =="WEST":
            x-=1
        if 0<=x<=5 and 0<=y<=5:
            return True
        else:
            print("Invalid move, your Pacman remains in the same position at {}, {}, {}".format(self.position[0],self.position[1], self.facing))
            return False
        
    def left(self):
        """ 
        Changes direction of Pacman 90 degrees on the board to the left
        
        """  
        if self.facing =="NORTH":
            self.facing ="WEST"
        elif self.facing =="EAST":
            self.facing = "NORTH"
        elif self.facing =="SOUTH":
            self.facing = "EAST"
        elif self.facing =="WEST":
            self.facing = "SOUTH"
            
    def right(self):
        """ 
        Changes direction of Pacman 90 degrees on the board to the right 
        
        """ 
        if self.facing =="NORTH":
            self.facing ="EAST"
        elif self.facing =="EAST":
            self.facing = "SOUTH"
        elif self.facing =="SOUTH":
            self.facing = "WEST"
        elif self.facing =="WEST":
            self.facing = "NORTH"
    
    def get_position(self):
        """ 
        Returns the current position of Pacman
        
        Returns:
        list: The co-ordinates of the Pacman
        """
        return self.position
    
    def report(self):
        """ 
        Prints the Pacmans position in x,y co-ordinates and the direction Pacman is facing
        
        """
        print("Your pacman is in position {},{}, {}".format(self.position[0],self.position[1], self.facing))
               
def main():
    
    p = pacman()
    is_valid = True
    is_placed = False
    directions = ["NORTH", "SOUTH", "EAST","WEST"]
    cmds = ["MOVE","LEFT","RIGHT","REPORT"]
    
    while(is_valid):
        input_str = input()
        valid_facing = False
        valid_input = False
        
        # This if statement uses regex to check if the PLACE command was inputted correctly
        if re.findall("PLACE [0-5],[0-5],*", input_str): 
            facing = input_str[10:]    
            
            for direction in directions:
                if facing == direction:
                    valid_input = True
                    valid_facing = True
            
            if valid_facing:
                x = int(input_str[6:7])
                y = int(input_str[8:9])
                f = input_str[10:]
                p.place(x,y,f)
                is_placed = True

        if is_placed:
            
            for cmd in cmds:
                if input_str == cmd:
                    valid_input = True 
                    
            if input_str == cmds[0]:
                valid_move = p.check()
                p.move(valid_move)
            if input_str == cmds[1]:
                p.left()
            if input_str == cmds[2]:
                p.right()
            if input_str == cmds[3]:
                p.report()
                
        if input_str == "END":
            is_valid = False
            #print(is_valid)
        
        elif not valid_input:
            
            for cmd in cmds:
                if input_str == cmd:
                    print("you need to PLACE the Pacman before {} command".format(input_str))
                    
            print("Please type an allowed command")
    print("end of program")

if __name__ == '__main__':
    main()
        


