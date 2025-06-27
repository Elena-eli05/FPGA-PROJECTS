module TFF(clk,T,Q);

input clk;
input T;
output reg Q;
initial Q=0;
always@(posedge clk)
    begin
        if (T)
            Q=~Q;
        else
            Q=Q;
    end
endmodule
