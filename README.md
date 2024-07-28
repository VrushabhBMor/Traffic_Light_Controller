# Traffic Light Controller
<details>
   <summary>Task - 1 -> Using Xilinx Vivado software, I developed the verilog code for the controller.</summary>
   
## Verilog code
    `timescale 1ns / 1ps
    module Traffic_Light_Controller(
        input clk,rst,
        output reg [2:0]light_M1,
        output reg [2:0]light_S,
        output reg [2:0]light_MT,
        output reg [2:0]light_M2
        );
        reg clock_out;
        reg [28:0] cnt=29'd0;
    parameter Divisor=29'd200000000;
    always@(posedge clk)
    begin
    cnt<=cnt+29'd1;
    if(cnt>=(Divisor-1))
    cnt<=29'd0;
    clock_out<=(cnt<Divisor/2)?1'b1:1'b0;
    end
    
        parameter  S1=0, S2=1, S3 =2, S4=3, S5=4,S6=5;
        reg [3:0]count;
        reg[2:0] ps;
        parameter  sec7=7,sec5=5,sec2=2,sec3=3;
    
       
        
        always@(posedge clock_out or posedge rst)
            begin
            if(rst==1)
            begin
            ps<=S1;
            count<=0;
            end
            else
                case(ps)
                    S1: if(count<sec7)
                            begin
                            ps<=S1;
                            count<=count+1;
                            end
                        else
                            begin
                            ps<=S2;
                            count<=0;
                            end
                    S2: if(count<sec2)
                            begin
                            ps<=S2;
                            count<=count+1;
                            end
    
                        else
                            begin
                            ps<=S3;
                            count<=0;
                            end
                    S3: if(count<sec5)
                            begin
                            ps<=S3;
                            count<=count+1;
                            end
    
                        else
                            begin
                            ps<=S4;
                            count<=0;
                            end
                    S4:if(count<sec2)
                            begin
                            ps<=S4;
                            count<=count+1;
                            end
    
                        else
                            begin
                            ps<=S5;
                            count<=0;
                            end
                    S5:if(count<sec3)
                            begin
                            ps<=S5;
                            count<=count+1;
                            end
    
                        else
                            begin
                            ps<=S6;
                            count<=0;
                            end
    
                    S6:if(count<sec2)
                            begin
                            ps<=S6;
                            count<=count+1;
                            end
    
                        else
                            begin
                            ps<=S1;
                            count<=0;
                            end
                    default: ps<=S1;
                    endcase
                end   
    
                always@(ps)    
                begin
                    
                    case(ps)
                         
                        S1:
                        begin
                           light_M1<=3'b001;
                           light_M2<=3'b001;
                           light_MT<=3'b100;
                           light_S<=3'b100;
                        end
                        S2:
                        begin 
                           light_M1<=3'b001;
                           light_M2<=3'b010;
                           light_MT<=3'b100;
                           light_S<=3'b100;
                        end
                        S3:
                        begin
                           light_M1<=3'b001;
                           light_M2<=3'b100;
                           light_MT<=3'b001;
                           light_S<=3'b100;
                        end
                        S4:
                        begin
                           light_M1<=3'b010;
                           light_M2<=3'b100;
                           light_MT<=3'b010;
                           light_S<=3'b100;
                        end
                        S5:
                        begin
                           light_M1<=3'b100;
                           light_M2<=3'b100;
                           light_MT<=3'b100;
                           light_S<=3'b001;
                        end
                        S6:
                        begin 
                           light_M1<=3'b100;
                           light_M2<=3'b100;
                           light_MT<=3'b100;
                           light_S<=3'b010;
                        end
                        default:
                        begin 
                           light_M1<=3'b000;
                           light_M2<=3'b000;
                           light_MT<=3'b000;
                           light_S<=3'b000;
                        end
                        endcase
                end                
                  
    
    endmodule
### Task 1 finished
</details>

---

<details>
   <summary>Task - 2 -> Writing testbench for the controller.</summary>
   
## Testbench
    `timescale 1ns / 1ps
    module Traffic_Light_Controller_TB;
    reg clk,rst;
    wire [2:0]light_M1;
    wire [2:0]light_S;
    wire [2:0]light_MT;
    wire [2:0]light_M2;
    Traffic_Light_Controller dut(.clk(clk) , .rst(rst) ,
     .light_M1(light_M1) , .light_S(light_S)  ,
     .light_M2(light_M2),.light_MT(light_MT)   );
    initial begin
        clk=1'b0;
        forever #(1000000000/2) clk=~clk;
    end
    //    initial
    //    $stop;//to add ps
    initial begin
        rst=0;
        #1000000000;
        rst=1;
        #1000000000;
        rst=0;
        #(1000000000*200);
        $finish;
        end
    endmodule

## Task 2 completed

</details>

---

<details>
   <summary>Results and the overview of the project</summary>
Please find the attached pdf file named "Traffic
</details>
