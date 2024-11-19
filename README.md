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

module Traffic_Light_Controller_tb;

    // Inputs
    reg clk;
    reg rst;

    // Outputs
    wire [2:0] light_M1;
    wire [2:0] light_S;
    wire [2:0] light_MT;
    wire [2:0] light_M2;

    // Instantiate the Traffic_Light_Controller module
    Traffic_Light_Controller uut (
        .clk(clk),
        .rst(rst),
        .light_M1(light_M1),
        .light_S(light_S),
        .light_MT(light_MT),
        .light_M2(light_M2)
    );

    // Clock generation
    always begin
        #5 clk = ~clk;  // Generate a clock with period of 10ns (100MHz)
    end

    // Initial block to apply test vectors
    initial begin
        // Initialize signals
        clk = 0;
        rst = 0;
        
        // Apply reset
        rst = 1;
        #20;   // Hold reset for 20ns
        rst = 0;

        // Wait for some time to observe the behavior
        #1000;  // Simulate for 1000ns
        
        // Apply a reset again
        rst = 1;
        #20;   // Hold reset for 20ns
        rst = 0;

        // Simulate further to observe reset behavior
        #1000;  // Simulate for another 1000ns

        // Finish the simulation
        $finish;
    end

    // Monitor the outputs to print their values during simulation
    initial begin
        $monitor("Time = %0t | light_M1 = %b, light_M2 = %b, light_MT = %b, light_S = %b", 
                 $time, light_M1, light_M2, light_MT, light_S);
    end

## Task 2 completed

</details>

---

<details>
   <summary>Results and the overview of the project</summary>
Please find the attached pdf file named "Traffic Light Controller.pdf" for the overview of the project and the simulation results.
</details>
