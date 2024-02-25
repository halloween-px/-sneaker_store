<script>
import axios from "axios";

const path = "https://43613f267f4ff091.mokky.dev/items";
const getData = async (url) => {
  try{
    const {data} = await axios.get(url)
    return data;
  }
  catch (err) {
    console.log(err)
  }
}

export const getProduct = async (id) => {
  return await getData(`${path}/${id}`);
}

export const getProducts = async () => {
  return await getData(path);
}

export const filtersProduct = async (filter, sort) => {
  const prefix = filter ? '&' : '';
  const title = filter ? `title=*${filter}*` : '';
  const sorting = sort ? `${prefix}sortBy=${sort}` : '';
  return await getData(`${path}?${title}${sorting}`);
}

export const sortProduct = async (sort) => {
  return await getData(`${path}?sortBy=${sort}`);
}

export const searchProduct = async (value, sort) => {
  const sorting = sort ? `&sortBy=${sort}` : '';
  return await getData(`${path}?title=*${value}*${sorting}`);
}

export const searchKeyWord = (items, value) => {
  items.value.forEach(el => {
    const indexFont = el.title.indexOf(value);
    const strElement = new RegExp(value, 'gi');
    const newStr = String(strElement).replace(/\/|\(\?:\)|gi/gi, "");
    let capitalizedStr = null;
    if(el.title[indexFont] !== value[0]) {
      capitalizedStr = newStr.charAt(0).toUpperCase() + newStr.slice(1);
    }
    el.title = el.title.replace(strElement, `<span class="search-text">${capitalizedStr ? capitalizedStr : newStr}</span>`);
  })
}
</script>