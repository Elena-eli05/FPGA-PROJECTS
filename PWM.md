module pwm(
    input clk,
    input rst,
    input a_25,
    input b_50,
    input c_75,
    output reg y1,
    output reg y2,
    output reg y3,
    output reg [7:0] count
    );

    

    always @(posedge clk) begin
        if (rst)
            count <= 8'b00000000;
        else begin
            count <= count + 1;

            // PWM for 25%
            if (a_25) begin
                if (count < 64)
                    y1 <= 1;
                else 
                    y1 <= 0;
            end
            else y1 <= 0;

            // PWM for 50%
            if (b_50) begin
                if (count < 128)
                    y2 <= 1;
                else 
                    y2 <= 0;
            end
            else y2 <= 0;

            // PWM for 75%
            if (c_75) begin
                if (count < 192)
                    y3 <= 1;
                else 
                    y3 <= 0;
            end
            else y3 <= 0;
        end
    end
endmodule
