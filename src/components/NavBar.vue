<template>
  <div>
    <nav class="nav" :style="{background: background || 'red'}">
      <ul class="nav-items" :style="{background: background || 'red'}" ref="nav">
        <figure>
          <img src="@/assets/logo.png" alt="" height="40px" width="40px" 
            @click="toggle"
          >
        </figure>
        <li v-for="(link,index) in navLinks" 
          :key="index"
          @click="toggle"
          @mouseenter="$event.currentTarget.style.background = hoverBackground || '#999'"
				  @mouseleave="$event.currentTarget.style.background = background || '#333'"
        >
          <router-link 
            :to="link.path"
            :style="{ color: linkColor || 'green' }"            
          >
            {{link.text}}
            <i :class="link.icon"></i>
          </router-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: ["navLinks", "linkColor","background","hoverBackground"],
  methods: {
		toggle () {
      const nav = this.$refs.nav.classList
      nav.contains('active') ? nav.remove('active') : nav.add('active')
		}
	}
};
</script>
<style scoped>
nav {
  height: 60px;
  width: 100%;
  box-shadow: 2px 2px 2px #ccc;
}
figure{
  cursor: pointer;
  margin-left: 10px;
}
ul{
  display: flex;
  height: 100%;
  align-items: center;
  list-style: none;
  transition: 300ms ease all;
  box-shadow: 2px 2px 2px #ccc;
}
i{
  display: flex;
  align-items: center;
  margin-right: 10px;
  font-size: 20px;
}
a{
  text-decoration: none;
  list-style: none;
  display: flex;
  flex-direction: row-reverse;
}
li{
  padding: 10px 20px;
}

@media screen and (max-width: 759px) {
  ul{
    position: absolute;
    width:300px;
    flex-direction: column;
    top:60px;
    left:-240px; 
    
  }
  figure{
    position: fixed;
    z-index: 1;
    top:10px;
    left:8px;
    margin-left: 0;
  }
  li{
    width: 100%;
    padding-left:0px;
    padding-right: 0px;
  }
  a{
    flex-direction: row;
    margin-left: 20px;
    justify-content: space-between;
    margin-right: 10px;
  }
  .active{
    left: 0px;
  }
}
</style>
