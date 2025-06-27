module updown_counter(clk,rst,updwn,count);

input clk,rst,updwn;
output reg[3:0] count;
always@(posedge clk or posedge rst)
begin
if(rst)
count<=4'b0000;
else if(updwn)
count<=count+1'b1;
else
count<=count-1'b1;
end
endmodule
