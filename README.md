Design code:

module encoder42 (
    input [3:0] in,      
    output reg [1:0] out, 
    output reg valid      
);

always @(*) begin
    case (in)
        4'b0001: begin
            out = 2'b00; 
            valid = 1'b1;
        end
        4'b0010: begin
            out = 2'b01; 
            valid = 1'b1;
        end
        4'b0100: begin
            out = 2'b10; 
            valid = 1'b1;
        end
        4'b1000: begin
            out = 2'b11; 
            valid = 1'b1;
        end
        default: begin
            out = 2'b00; 
            valid = 1'b0;
        end
    endcase
end
endmodule


Test bench :

`timescale 1ns/1ps

module encoder42_tb();
reg [3:0] in;        
wire [1:0] out;     
wire valid;        
encoder42 uut (
    .in(in),
    .out(out),
    .valid(valid)
);
initial 
begin
    $monitor("Time = %0t | Input = %b | Output = %b | Valid = %b", $time, in, out, valid);
    in = 4'b0001; #10;
    in = 4'b0010; #10;
    in = 4'b0100; #10;
    in = 4'b1000; #10;
    in = 4'b0000; #10;
    in = 4'b0110; #10;
    $finish();
end
endmodule


