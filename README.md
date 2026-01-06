import pandas as pd
import re

def standardize_company_name(company_name):
    """
    Standardize company name to "CAF SoftSol India Pvt Ltd."
    
    Parameters:
    company_name (str): Company name to be standardized
    
    Returns:
    str: Standardized company name
    """
    if pd.isnull(company_name):
        return ""
    
    # Define mapping for variations
    company_name_map = {
        r"CAF\s*(softsol|solution|softSolution).*": "CAF SoftSol India Pvt Ltd."
    }
    
    # Iterate through mapping and replace
    for pattern, replacement in company_name_map.items():
        if re.match(pattern, company_name, re.IGNORECASE):
            return replacement
    
    # If no match, return original value
    return company_name

# Example usage
df = pd.DataFrame({
    "Company Name": ["CAF softsol", "CAF solution", "CAF softSolution India Pvt Limited", None, "Invalid Company"]
})

df["Standardized Company Name"] = df["Company Name"].apply(standardize_company_name)

print(df)
