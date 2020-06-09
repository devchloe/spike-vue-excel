<template>
  <ul class="nav nav-tabs header-tabs">
    <li class="nav-item">
      <a href="team-overview.html" class="nav-link active">
        Overview
      </a>
    </li>
    <li class="nav-item">
      <a href="team-projects.html" class="nav-link ">
        Projects
      </a>
    </li>
    <li class="nav-item">
      <a href="team-members.html" class="nav-link">
        Members
      </a>
    </li>
    <li class="nav-item">
      <a href="#!" class="nav-link">
        Settings
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  name: "NavigationTabs"
};
</script>

<style scoped>
ul,
li {
  list-style: none;
}

a {
  text-decoration: none;
}
.nav {
  display: flex;
  align-items: center;
}

.nav-overflow {
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  padding-bottom: 1px; /*border bottom이 안보일 수 있음, 가려져서 */

  /* &::-webkit-scrollbar {*/
  /*  display: none;*/
  /*}*/
}
.nav-item {
  margin-left: 1em;
  margin-right: 1em;
}

.nav-item:first-child {
  margin-left: 0;
}
.nav-item:last-child {
  margin-right: 0;
}
.nav-link {
  padding: 1em 0;
  border-bottom: 2px solid transparent;
  border-left-width: 0;
  border-right-width: 0;
  border-top-width: 0;

  /*&:not(.active) {*/
  /*  color: grey*/

  /*  &:hover {*/
  /*    color: blue;*/
  /*  }*/
  /*}*/
}

.nav-link:not(.active) {
  color: grey;
}

.nav-link:not(.active):hover {
  color: blueviolet;
}

.active {
  border-bottom: 2px solid blue;
}
</style>
