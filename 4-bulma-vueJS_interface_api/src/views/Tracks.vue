<template>
  <ViewList ref="viewList"/>
</template>

<script>
import ViewList from "@/components/view/list/ViewList.vue";
export default {
  name: 'Tracks',
  components: {ViewList},
  data()
  {
    return {
      sorts: [
        {fullName: "Name", shortName: "Name"},
        {fullName: "Unit Price", shortName: "UnitPrice"},
        {fullName: "Duration", shortName: "Milliseconds"},
        {fullName: "Composer", shortName: "Composer"},
        {fullName: "Track Id", shortName: "TrackId"},
        {fullName: "Album Id", shortName: "AlbumId"},
        {fullName: "Genre Id", shortName: "GenreId"},
        {fullName: "Media Type", shortName: "MediaTypeId"},
      ],

      identifier: "TrackId",

      cards: {
        title: {
          name: "Name",
          // label: "Name",
          pre: "",
          post: "",
        },
        subtitle: {
          name: "UnitPrice",
          pre: "$",
          post: ""
        },
        infos: [
          {
            name: "Milliseconds",
            pre: "",
            post: ""
          },
          {
            name: "Composer",
            pre: "Compositeur(s): ",
            post: ""
          }],
      },

      formView: [
          [{name: "Name", label: "Title", icon:"", placeholder:"Title", type:"text", classes: "is-large"}],
          [{name: "UnitPrice", label: "Price", icon:"fa fa-dollar", placeholder: "e.g. 22.99", type:"number"}, {name: "Milliseconds", label: "Duration (minutes)", icon:"", placeholder: "e.g. 1.8", type:"number"}],
          [{name: "Composer", label: "Composers (comma separated)", icon:"", placeholder:"e.g. Mozart", type:"area"}],
      ]
    }
  },
  mounted() {
    this.$refs.viewList.setView("tiles");
    this.$refs.viewList.setSortOptions(this.sorts);
    this.$refs.viewList.setModel(this.cards);
    this.$refs.viewList.setDataSet("tracks");
    this.$refs.viewList.setIdentifier(this.identifier);
    this.$refs.viewList.setPageTitle("Tracks");
    this.$refs.viewList.setSearchComponent(["Name", "Composer"], "Titre, compositeur...", "Search");
    this.$refs.viewList.setCounterComponent("tracks");
    this.$refs.viewList.setFormView(this.formView);
    this.$refs.viewList.setExcludedProps(["Sold"]);

    // this.$refs.viewList.setCardsTitle("Name");
    this.$refs.viewList.init();
  },
}
</script>

