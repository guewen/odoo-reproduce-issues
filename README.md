# Odoo issues

Each branch contains a small addon allowing to reproduce a bug.
These modules have no purpose other than debugging.

## Issue with "compute qty at date extensibility"

1. install the module "compute_qty_at_date"
2. install "sale management"
3. create a sale order
4. select a product
5. empty the product field

Result: 

```
  File "/odoo/odoo/models.py", line 6056, in onchange
    snapshot0 = Snapshot(record, nametree)
  File "/odoo/odoo/models.py", line 5942, in __init__
    self.fetch(name)
  File "/odoo/odoo/models.py", line 5952, in fetch
    self[name] = record[name]
  File "/odoo/odoo/models.py", line 5610, in __getitem__
    return self._fields[key].__get__(self, type(self))
  File "/odoo/odoo/fields.py", line 1020, in __get__
    self.compute_value(recs)
  File "/odoo/odoo/fields.py", line 1105, in compute_value
    records._compute_field_value(self)
  File "/odoo/odoo/models.py", line 3915, in _compute_field_value
    getattr(self, field.compute)()
  File "/odoo/addons/compute_qty_at_date/models/sale_order_line.py", line 11, in _compute_qty_at_date
    return super()._compute_qty_at_date()
  File "/odoo/addons/sale_stock/models/sale_order.py", line 262, in _compute_qty_at_date
    qty_available_today, free_qty_today, virtual_available_at_date = qties_per_product[line.product_id.id]
KeyError: False
```
