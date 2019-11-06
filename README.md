# Calculator_Temp_Part2




  case 3:
                        MortgageCalculator mc = new MortgageCalculator();
                        Console.WriteLine("Mortgage Calculator \r");
                        Console.WriteLine("-----------------------\n");
                        Console.Write("Enter the property price: ");
                        decimal purchasePrice = Convert.ToDecimal(Console.ReadLine());
                        Console.Write("Enter the downpayment amount: ");
                        decimal downPayment = Convert.ToDecimal(Console.ReadLine());
                        
                        mc.CalculatePayment();
                        mc.InterestRate = 3.5;
                        mc.LoanTermYears = 30;
                        DisplayLoanInformation(mc);

                        void DisplayLoanInformation(MortgageCalculator mc)
                        {
                            Console.WriteLine("Purchase Price: {0:C}", mc.purchasePrice);
                            Console.WriteLine("Down Payment: {0:C}", mc.downPayment);
                            Console.WriteLine("Loan Amount: {0:C}", mc.LoanAmount);
                            Console.WriteLine("Annual Interest Rate: {0}%", mc.InterestRate);
                            Console.WriteLine("Term: {0} years ({1} months)", mc.LoanTermYears, mc.LoanTermMonths);
                            Console.WriteLine("Monthly Payment: {0:C}", mc.CalculatePayment());
                            Console.WriteLine();
                        }
                        Console.WriteLine("------------------------\n");
                        break;
                }
                continue;
            }
   
  



    public class MortgageCalculator
        {
            private const int MonthsPerYear = 12;
            public decimal purchasePrice;
            public decimal downPayment;

            public MortgageCalculator()
            {
            }

            public MortgageCalculator(string inputPurchasePrice, string inputDownPayment)
            {
                purchasePrice = Decimal.Parse(inputPurchasePrice);
                downPayment = Decimal.Parse(inputDownPayment);
            }

            public MortgageCalculator(decimal purchasePrice, decimal downPayment)
            {
                this.purchasePrice = purchasePrice;
                this.downPayment = downPayment;
              
            }


            public decimal LoanAmount
            {
                get { return (purchasePrice - downPayment); }
            }

            public double InterestRate;


            public double LoanTermMonths;


            public double LoanTermYears
            {
                get { return LoanTermMonths / MonthsPerYear; }
                set { LoanTermMonths = (value * MonthsPerYear); }
            }


            // Calculates the monthy payment amount based on current
            // <returns>Returns the monthly payment amount</returns>
            public decimal CalculatePayment()
            {
                decimal payment = 0;

                if (LoanTermMonths > 0)
                {
                    if (InterestRate != 0)
                    {
                        double rate = ((InterestRate / MonthsPerYear) / 100);
                        double factor = (rate + (rate / (Math.Pow(rate + 1, LoanTermMonths) - 1)));
                        payment = (LoanAmount * (decimal)factor);
                    }
                    else payment = (LoanAmount / (decimal)LoanTermMonths);
                }
                return Math.Round(payment, 2);
            }

        }
