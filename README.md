class Product {
  static #list = [] 

  constructor(name, price, description) {
    this.id = Math.floor(Math.random() * (99999 - 10000 + 1)) + 10000;
    // this.id = new Date().getTime();
    this.name = name
    this.price = price
    this.description = description
  }

  static add = (product) => {
    this.#list.push(product)
  }
  
  static getList = () => this.#list;
  
  static getById = (id) =>
  this.#list.find((product) => product.id === id)
  
  static deleteById = (id) => {
    const index = this.#list.findIndex((product) => product.id === id);
    if (index !== -1) {
      this.#list.splice(index, 1); 
      return true; 
    }
    return false; 
  };
}

router.get('/product-delete', function (req, res) {
  const { id } = req.query;
  const isDeleted = Product.deleteById(Number(id));
  
  if (isDeleted) {
    res.render('alert', {
      style: 'alert',
      info1: 'Успішне виконання дії',
      info4: 'Товар видалений',
    });
  } else {
    res.render('alert', {
      style: 'alert',
      info1: 'Помилка',
      info4: 'Товар не знайдено',
    });
  }
});
