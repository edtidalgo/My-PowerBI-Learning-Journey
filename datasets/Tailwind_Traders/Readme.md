<!-- TailwindTradersDB ERD (HTML tables) -->

<h2>TailwindTradersDB – Entities</h2>

<table>
  <thead>
    <tr>
      <th colspan="2">Customers</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>CustomerID</td><td>PK</td></tr>
    <tr><td>CustomerName</td><td>Text</td></tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th colspan="2">Products</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>SKU</td><td>PK</td></tr>
    <tr><td>ProductName</td><td>Text</td></tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th colspan="2">Countries</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>CountryID</td><td>PK</td></tr>
    <tr><td>Country</td><td>Text</td></tr>
    <tr><td>ExchangeID</td><td>Number</td></tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th colspan="2">Suppliers</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>SupplierID</td><td>PK</td></tr>
    <tr><td>SupplierName</td><td>Unique Text</td></tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th colspan="2">Sales</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>OrderID</td><td>PK</td></tr>
    <tr><td>CustomerID</td><td>FK → Customers.CustomerID</td></tr>
    <tr><td>SKU</td><td>FK → Products.SKU</td></tr>
    <tr><td>CountryID</td><td>FK → Countries.CountryID</td></tr>
    <tr><td>OrderDate</td><td>Date</td></tr>
    <tr><td>Quantity</td><td>Number</td></tr>
    <tr><td>Price</td><td>Number</td></tr>
  </tbody>
</table>

<table>
  <thead>
    <tr>
      <th colspan="2">Purchases</th>
    </tr>
    <tr>
      <th>Column</th>
      <th>Details</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>PurchaseID</td><td>PK</td></tr>
    <tr><td>SupplierID</td><td>FK → Suppliers.SupplierID</td></tr>
    <tr><td>OrderID</td><td>FK → Sales.OrderID</td></tr>
    <tr><td>LastVisited</td><td>Date</td></tr>
    <tr><td>ReturnStatus</td><td>Text</td></tr>
    <tr><td>WarrantyMonths</td><td>Number (CHECK > 0)</td></tr>
    <tr><td>PurchaseDate</td><td>Date</td></tr>
    <tr><td>ReturnPolicyDays</td><td>Number (CHECK 0–60)</td></tr>
    <tr><td>Feedback</td><td>Text</td></tr>
  </tbody>
</table>

<h2>Relationships</h2>

<table>
  <thead>
    <tr>
      <th>From table</th>
      <th>Foreign key</th>
      <th>To table</th>
      <th>Reference</th>
      <th>Cardinality</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sales</td>
      <td>CustomerID</td>
      <td>Customers</td>
      <td>Customers.CustomerID</td>
      <td>Many Sales per Customer</td>
    </tr>
    <tr>
      <td>Sales</td>
      <td>SKU</td>
      <td>Products</td>
      <td>Products.SKU</td>
      <td>Many Sales per Product</td>
    </tr>
    <tr>
      <td>Sales</td>
      <td>CountryID</td>
      <td>Countries</td>
      <td>Countries.CountryID</td>
      <td>Many Sales per Country</td>
    </tr>
    <tr>
      <td>Purchases</td>
      <td>SupplierID</td>
      <td>Suppliers</td>
      <td>Suppliers.SupplierID</td>
      <td>Many Purchases per Supplier</td>
    </tr>
    <tr>
      <td>Purchases</td>
      <td>OrderID</td>
      <td>Sales</td>
      <td>Sales.OrderID</td>
      <td>Zero/One Purchase per Sale (as modeled)</td>
    </tr>
  </tbody>
</table>
