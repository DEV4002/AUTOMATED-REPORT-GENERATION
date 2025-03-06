import pandas as pd
from reportlab.lib.pagesizes import letter
from reportlab.pdfgen import canvas
from reportlab.lib import colors
from reportlab.platypus import SimpleDocTemplate, Table, TableStyle, Spacer, Paragraph
from reportlab.lib.styles import getSampleStyleSheet

# Read data from CSV file
data = pd.read_csv("C:\\Users\\asus\\OneDrive\\Desktop\\ALLPROJECT\\CODTECH INTERNSHIP\\REPORT GENERATION\\BOOK.CSV")

# Data Analysis: Calculate average salary
average_salary = data['Salary'].mean()

# Create PDF report
def generate_pdf_report(data, average_salary):
    pdf_file = "report.pdf"
    doc = SimpleDocTemplate(pdf_file, pagesize=letter)
    elements = []

    # Table Data
    table_data = [data.columns.tolist()] + data.values.tolist()

    # Create Table
    table = Table(table_data)
    table.setStyle(TableStyle([
        ('BACKGROUND', (0, 0), (-1, 0), colors.grey),
        ('TEXTCOLOR', (0, 0), (-1, 0), colors.whitesmoke),
        ('ALIGN', (0, 0), (-1, -1), 'CENTER'),
        ('FONTNAME', (0, 0), (-1, 0), 'Helvetica-Bold'),
        ('BOTTOMPADDING', (0, 0), (-1, 0), 12),
        ('BACKGROUND', (0, 1), (-1, -1), colors.beige),
        ('GRID', (0, 0), (-1, -1), 1, colors.black),
    ]))

    elements.append(table)

    # Add Analysis Result
    elements.append(Spacer(1, 12))
    
    # Get sample style for Paragraph
    styles = getSampleStyleSheet()
    style = styles['Normal']
    
    elements.append(Paragraph(f"Average Salary: {average_salary:.2f}", style))

    # Build PDF
    doc.build(elements)

# Generate PDF report
generate_pdf_report(data, average_salary)
