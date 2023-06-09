<template>
  <div class="items">
    <h1 class="title">Items</h1>

    <nav class="level">
      <div class="level-left">
        <div class="level-item">
          <p class="subtitle is-5">
            <strong>{{this.items.length}}</strong> / {{this.allItems.length}} items
          </p>
        </div>

        <p class="level-item">
          <button class="button is-success" @click="callNewItem">New</button>
        </p>

        <div class="level-item is-hidden-tablet-only">
          <div class="field has-addons">
            <p class="control">
              <input class="input" type="text" placeholder="Item name, ISBN…" v-model="searchWord" v-on:keyup="search">
            </p>
            <p class="control">
              <button class="button" @click="search">Search</button>
            </p>
          </div>
        </div>
      </div>

      <div class="level-right">
        <div class="level-item">
          Order by
        </div>
        <div class="level-item">
          <div class="select">
            <select @change="sortItems">
              <option value="publishDate">Publish date</option>
              <option value="price">Price</option>
              <option value="pageCount">Page count</option>
            </select>
          </div>
        </div>
      </div>
    </nav>

    <div class="columns is-multiline">
      <template v-for="(item, key) in items">
        <div class="column is-12-tablet is-6-desktop is-4-widescreen">
          <article class="box">
            <div class="media">
              <aside class="media-left">
                <img :src="require(`@/assets/images/${item.coverImage}`)" width="80">
              </aside>
              <div class="media-content">
                <p class="title is-5 is-spaced is-marginless">
                  <a @click="callEditItem(item)">{{item.Name}}</a>
                </p>
                <p class="subtitle is-marginless">
                  ${{item.price}}
                </p>
                <div class="content is-small">
                  {{item.pageCount}} pages
                  <br>
                  ISBN: {{item.ISBN}}
                  <br>
                  <a @click="callEditItem(item)">Edit</a>
                  <span> | </span>
                  <a @click="deleteItem(item)">Delete</a>
                </div>
              </div>
            </div>
          </article>
        </div>
      </template>

    </div>

    <nav class="pagination">
      <a class="pagination-previous">Previous</a>
      <a class="pagination-next">Next page</a>
      <ul class="pagination-list">
        <li>
          <a class="pagination-link">1</a>
        </li>
        <li>
          <span class="pagination-ellipsis">&hellip;</span>
        </li>
        <li>
          <a class="pagination-link">45</a>
        </li>
        <li>
          <a class="pagination-link is-current">46</a>
        </li>
        <li>
          <a class="pagination-link">47</a>
        </li>
        <li>
          <span class="pagination-ellipsis">&hellip;</span>
        </li>
        <li>
          <a class="pagination-link">86</a>
        </li>
      </ul>
    </nav>
  </div>
  <ModalItem ref="modalItem" :show-modal="showNewModal" @close="showNewModal = false" @sent-data="addItem" @edit-data="editItem"></ModalItem>
</template>

<script>
import Collect from 'collect.js';
import ModalItem from "@/components/ModalItem.vue";

export default {
  name: 'Items',
  components: {ModalItem},
  data() {
    return {
      items: [],
      allItems: [
        {
          Name: "TensorFlow For Machine Intelligence",
          price: "22.99",
          pageCount: 270,
          ISBN: "9781939902351",
          coverImage: "tensorflow.jpg",
          publishDate: 2017,
        },
        {
          Name: "Docker in Production",
          price: "22.99",
          pageCount: 156,
          ISBN: "9781939902184",
          coverImage: "docker.jpg",
          publishDate: 2015,
        },
        {
          Name: "Learning Swift",
          price: "22.99",
          pageCount: 342,
          ISBN: "9781939902115",
          coverImage: "swift.jpg",
          publishDate: 2015,
        },
        {
          Name: "Choosing a JavaScript Framework",
          price: "19.99",
          pageCount: 270,
          ISBN: "9781939902092",
          coverImage: "js-framework.jpg",
          publishDate: 2016,
        },
        {
          Name: "Developing a Gulp.js Edge",
          price: "22.99",
          pageCount: 134,
          ISBN: "9781939902146",
          coverImage: "gulp.jpg",
          publishDate: 2014,
        },
      ],
      item: {
        Name: "",
        price: "",
        pageCount: "",
        ISBN: "",
        coverImage: "",
        publishDate: "",
      },
      showNewModal: false,
      showEditModal: false,
      searchWord: "",
      currentItem: null,
    };
  },

  methods:
  {
    sortItems(event)
    {
      let selectValue = String(event.target.value);
      let collection = Collect(this.items);
      let sortedBooks = collection.sortBy(selectValue);

      this.items = Object.assign([], sortedBooks.all())
    },

    search() {
      if (this.searchWord === '') {
        this.items = this.allItems;
        return;
      }

      this.items = new Collect(this.allItems)
          .filter((item) => item.Name.toLowerCase().includes(this.searchWord.toLowerCase()))
          .all();
    },

    addItem(i)
    {
      this.items.push(i);
      this.showNewModal = false;
    },

    editItem(i)
    {
      for (let key in i) {
        this.currentItem[key] = i[key];
      }
      this.showNewModal = false;
      console.log(this.items)
    },

    callNewItem()
    {
      this.showNewModal = true;
      this.$refs.modalItem.newForm();
    },

    callEditItem(item)
    {
      this.showNewModal = true;
      this.$refs.modalItem.editForm(item);
      this.currentItem = item;
    },

    deleteItem(item)
    {
      this.items.splice(this.items.indexOf(item), 1);
    }
  },
  mounted() {
    this.items = this.allItems;
  }
}
</script>

<style lang="sass" scoped>

</style>