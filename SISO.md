module siso(clk,rst,D,Q);

input clk;
input rst;
input D;
output reg Q;
reg [3:0]shift;

always@(posedge clk)
    begin
        if(rst)
            shift<=4'b0000;
        else
         begin
            shift<={shift[2:0],D};
            Q<=shift[3];
         end
    end
    
endmodule
