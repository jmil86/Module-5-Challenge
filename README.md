# Module-5-Challenge
Pymaceuticals Analysis

Capomulin and Ramicane were the most effective drugs, demonstrating significantly smaller tumor volumes compared to the other treatments. Ketapril, on the other hand, was the least effective, resulting in larger tumor growth. Weight was a strong predictor of tumor size, with heavier mice consistently exhibiting larger tumors. This suggests that weight may play a role in tumor development and progression.


#### For this section, I utilized a combination of Xpert Learning Assistant and Chat GBT to help figure the structure of the code.
    # Put treatments into a list for for loop (and later for plot labels)
treatments = ["Capomulin", "Ramicane", "Infubinol", "Ceftamin"]


# Create empty list to fill with tumor vol data (for plotting)
tumor_vol_data = []


# Calculate the IQR and quantitatively determine if there are any potential outliers.
for treatment in treatments:


    # Locate the rows which contain mice on each drug and get the tumor volumes
    tumor_vol = final_tumor_volume.loc[final_tumor_volume["Drug Regimen"] == treatment, "Final Tumor Volume"]
    tumor_vol_data.append(tumor_vol)



    # add subset
    quartiles = tumor_vol.quantile([.25,.5,.75])
    lowerq = quartiles[0.25]
    upperq = quartiles[0.75]
    iqr = upperq-lowerq



    # Determine outliers using upper and lower bounds
    lower_bound = lowerq - (1.5*iqr)
    upper_bound = upperq + (1.5*iqr)
    outliers = tumor_vol.loc[(tumor_vol < lower_bound) | (tumor_vol > upper_bound)]
    print(f"{treatment} potential outliers: {outliers}")