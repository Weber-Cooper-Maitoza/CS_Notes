rename the Order table to OrderTable

synthetic keys:
- sdOrderTable_id
- sdCustomer_id
- sdSupplier_id
- sdProduct_id
- sdVendor_id


OrderTable
sdOrderTable_id PK
sdCustomer_id FK AK1
orderDateTime AK1/
subtotal NULL
shippingCost NULL
taxAmount NULL
orderTotal NULL