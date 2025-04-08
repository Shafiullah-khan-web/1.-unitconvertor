# 1.-unitconvertor
# prompt: Build a Google Unit Convertor using Python and Streamlit:

import streamlit as st

st.title("Google Unit Converter")

# Unit options
units = {
    "Length": ["Meters", "Kilometers", "Miles", "Feet", "Inches", "Centimeters"],
    "Weight": ["Kilograms", "Pounds", "Grams", "Ounces"],
    "Temperature": ["Celsius", "Fahrenheit", "Kelvin"],
    "Volume": ["Liters", "Gallons", "Cubic Meters", "Cubic Feet"]
}

selected_category = st.selectbox("Select a category", list(units.keys()))
from_unit = st.selectbox("Convert from", units[selected_category])
to_unit = st.selectbox("Convert to", units[selected_category])

value = st.number_input("Enter value", min_value=0.0, value=1.0)

def convert_units(value, from_unit, to_unit, category):
    if category == "Length":
        if from_unit == "Meters" and to_unit == "Kilometers":
            return value / 1000
        elif from_unit == "Meters" and to_unit == "Miles":
            return value * 0.000621371
        elif from_unit == "Meters" and to_unit == "Feet":
            return value * 3.28084
        elif from_unit == "Meters" and to_unit == "Inches":
            return value * 39.3701
        elif from_unit == "Meters" and to_unit == "Centimeters":
            return value * 100
        # Add more length conversions as needed
        else:
            return value  # Return original value if no conversion is found

    elif category == "Weight":
        if from_unit == "Kilograms" and to_unit == "Pounds":
            return value * 2.20462
        # Add more weight conversions as needed
        else:
            return value

    elif category == "Temperature":
        if from_unit == "Celsius" and to_unit == "Fahrenheit":
            return (value * 9/5) + 32
        elif from_unit == "Celsius" and to_unit == "Kelvin":
            return value + 273.15
        elif from_unit == "Fahrenheit" and to_unit == "Celsius":
            return (value - 32) * 5/9
        elif from_unit == "Fahrenheit" and to_unit == "Kelvin":
            return (value - 32) * 5/9 + 273.15
        elif from_unit == "Kelvin" and to_unit == "Celsius":
            return value - 273.15
        elif from_unit == "Kelvin" and to_unit == "Fahrenheit":
            return (value - 273.15) * 9/5 + 32
        # Add more temperature conversions as needed
        else:
            return value

    elif category == "Volume":
        # Add volume conversions as needed
        if from_unit == "Liters" and to_unit == "Gallons":
          return value * 0.264172
        else:
            return value
    else:
      return value

if st.button("Convert"):
    converted_value = convert_units(value, from_unit, to_unit, selected_category)
    st.write(f"{value} {from_unit} is equal to {converted_value} {to_unit}")
