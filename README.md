from prettytable import PrettyTable
"""
Library for create table
"""

class Transaction():

  def __init__(self):
    self.order = []

    """
    Function to initialize class Transaction
    ----------------------------------------
    self.order = list 
      attribute to put transaction data from add_item function in the form of list
    """


  def add_item(self, item_name, item_qty, item_price):

    """
    Function to add item for the transaction list
    ---------------------------------------------
    Parameters
    item_name = str
      Consist of the item name
    item_qty = float
      Quantity of the item to put in transaction
    item_price = float
      Price per item
    """
  
    # Check input type of item_qty and item_price
    try: 
      item_qty = float(item_qty)
      item_price = float(item_price)
    except ValueError as Error:
      raise ValueError ("Input Salah! Harus Angka!")
      return

    # Parameters
    self.item_name = item_name
    self.item_qty = item_qty
    self.item_price = item_price

    # Output (dict) will append the items to the list(self.order)
    items = {'nama': (item_name), "jumlah" : (item_qty), "harga" : (item_price)}
    self.order.append(items)   
    print(f"Berhasil memesan {item_name} berjumlah {item_qty} dengan harga Rp {item_price}.")
    return

   
  def update_item_name(self, item_name, new_name):

    """
    Function to change item name
    ----------------------------
    Parameters
    item_name = str
      Item name that will be changed
    new_name = str
      New name of the item
    """

    # Loop for find and change the item name

    found_items = list(filter(lambda items: items['nama'] == str(item_name), self.order))
    if len(found_items) > 0:
      found_items[0]['nama'] = str(new_name)
      print(f"{item_name} berhasil diubah menjadi {new_name}.")
    else:
      print("Item Tidak Ditemukan")      
 
  def update_item_qty(self, item_name, new_qty):
    
    """
    Function to change item quantity
    --------------------------------
    Parameters
    item_name = str
      Item which will be updated
    new_qty = float
      Updated quantity of the item
    """

    # Check the input type
    try:
      new_qty = float(new_qty)
    except ValueError as Error:
      raise ValueError ("Input Salah! Harus Angka Tanpa Kutip!")
      return

    found_items = list(filter(lambda items: items['nama'] == str(item_name), self.order))
    if len(found_items) > 0:
      found_items[0]['jumlah'] = float(new_qty)
      print(f"Jumlah {item_name} berhasil diubah menjadi {new_qty}.")
    else:
      print("Item Tidak Ditemukan")

  def update_item_price(self, item_name, new_price):

    """
    Function to change item price
    --------------------------------
    Parameters
    item_name = str
      Item which will be updated
    new_price = float
      Updated price of the item
    """

    # Check the input type
    try:
      new_price = float(new_price)
    except ValueError as Error:
      raise ValueError ("Input Salah! Harus Angka Tanpa Kutip!")
      return

    found_items = list(filter(lambda items: items['nama'] == str(item_name), self.order))
    if len(found_items) > 0:
      found_items[0]['harga'] = float(new_price)
      print(f"Harga {item_name} berhasil diubah menjadi {new_price}.")
    else:
      print("Item Tidak Ditemukan")

  def delete_item(self, item_name):
    
    """
    Function to delete item
    --------------------------------
    Parameters
    item_name = str
      Item which will be deleted
    """

    found_items = list(filter(lambda items: items['nama'] == str(item_name), self.order))
    if len(found_items) > 0:
      self.order.remove(found_items[0]) 
      print(f"Berhasil menghapus {item_name}.")
    else:
      print("Item Tidak Ditemukan")
             

  def reset_transaction(self):

    """
    Function to reset transaction
    --------------------------------
    Parameters
    item_name = str
      Item which will be updated
    new_price = float
      Updated price of the item
    """

    self.reset = self.order.clear()
    return print("Berhasil menghapus semua item")    

  def check_order(self):
    
    """
    Function to check the order with table form
    -------------------------------------------
    """

    try:
      x = PrettyTable()
      x.field_names = ["Item", "Jumlah", "Harga Satuan", "Total Harga"]
      x.align["Harga Satuan"] = "r" # Align to right
      x.align["Total Harga"] = "r" # Align to right
      
      for items in self.order:
        x.add_row([items['nama'], items['jumlah'], items['harga'], items['jumlah']*items['harga']])
      print(x)
    except:
      print("Belum ada transaksi")

  def print_total(self):

    """
    Function to see total transaction price
    Will get discounted if certain amount is achieved
    --------------------------------------------------
    """

    total_belanja = sum((items['jumlah']*items['harga']) for items in self.order)

    if total_belanja > 500_000:
      diskon = total_belanja * .08
      total_akhir = total_belanja - diskon
      print(f"Selamat! Anda mendapat potongan sebesar Rp {diskon}, total belanja Anda adalah Rp {total_akhir}.")

    elif total_belanja > 300_000:
      diskon = total_belanja * .05
      total_akhir = total_belanja - diskon
      print(f"Selamat! Anda mendapat potongan sebesar Rp {diskon}, total belanja Anda adalah Rp {total_akhir}.")

    elif total_belanja > 200_000:
      diskon = total_belanja * .02
      total_akhir = total_belanja - diskon
      print(f"Selamat! Anda mendapat potongan sebesar Rp {diskon}, total belanja Anda adalah Rp {total_akhir}.")

    elif total_belanja > 0:
      print(f"Total belanja Anda adalah Rp {total_belanja}.")
        
    else:
      print("Belum ada transaksi")

