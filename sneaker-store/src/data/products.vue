<script>
import axios from "axios";

const products = "https://43613f267f4ff091.mokky.dev/items";
const favorites = "https://43613f267f4ff091.mokky.dev/favorites";
const getData = async (url, params) => {
  try{
    const {data} = await axios.get(url, params)
    return data;
  }
  catch (err) {
    console.log(err);
  }
}

const postData = async (url, params) => {
  try{
    const {data} = await axios.post(url, params)
    return data;
  }
  catch (err) {
    console.log(err);
  }
}

export const deleteFavorite = async (id) => {
  await axios.delete(`${favorites}/${id}`)
}

export const getProducts = async () => {
  return await getData(products);
}

export const getFavorites = async () => {
  return await getData(favorites)
}

export const postFavorites = async (params) => {
  return await postData(favorites, params)
}

export const filtersProduct = async (filter, sort) => {
  const prefix = filter ? '&' : '';
  const title = filter ? `title=*${filter}*` : '';
  const sorting = sort ? `${prefix}sortBy=${sort}` : '';
  return await getData(`${products}?${title}${sorting}`);
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