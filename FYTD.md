# Fiscal Year To Date Functions
Works also with Fiscal Periods instead of Fiscal Months
<br>
```DAX
DEFINE

    FUNCTION f_CalculateFYTD = (
		// Fiscal Year To Date
				date_table : anyref,
				fiscal_year_field : anyref,
				fiscal_month_numb_field : anyref, -- can also be a period number
				metric : expr
			) =>
			
			VAR CurrentYear = MAX(fiscal_year_field)
			VAR CurrentMonthNum = MAX(fiscal_month_numb_field) 

			RETURN
			CALCULATE(
				metric,
				FILTER(
					ALL(date_table),
					fiscal_year_field = CurrentYear &&
					fiscal_month_numb_field <= CurrentMonthNum
				)
			)


	FUNCTION f_CalculateFYTD_PriorYear = (
		// Previous Year Fiscal Year To Date
				date_table : anyref,
				fiscal_year_field : anyref,
				fiscal_month_numb_field : anyref, -- can also be a period number
				metric : expr
			) =>
			
			VAR CurrentYear = MAX(fiscal_year_field)
			VAR CurrentMonthNum = MAX(fiscal_month_numb_field) 

			RETURN
			CALCULATE(
				metric,
				FILTER(
					ALL(date_table),
					fiscal_year_field = CurrentYear - 1 &&
					fiscal_month_numb_field <= CurrentMonthNum
				)
			)
```
