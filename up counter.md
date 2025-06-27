module upcounter(
    input clk,
    input rst,
    output [3:0]y
    );
	 
	 reg [3:0]y;
	 
	 always @(posedge clk or posedge rst)
	  begin
	    if (rst)
     		 y[3:0]<=4'b0000;
		 else 
		    y[3:0]<=y+1;
	  end

endmodule
