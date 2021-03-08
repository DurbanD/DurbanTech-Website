<template>
    <div id="nav">
        <router-link to='/' id='logo-link'><img alt="Durban Technology" src="../assets/Dtech_Logo_Small_Green_Silver.png"></router-link>
        <div id="navlinks">
            <router-link class="navlink" to="/" id="nav-home">Home</router-link>
            <router-link class="navlink" to="/about" id="nav-about">About</router-link>
            <router-link class="navlink" to="/contact" id="nav-contact">Contact</router-link>
        </div>
    </div>
</template>

<style>

img {
  max-height: 50px;
  background: var(--lightgreen-semitransparent);
  margin: 0;
}
#nav {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-content: center;
  align-items: center;
  height: auto;
  width: 90%;
  max-width: 100vw;
  padding: 5px 25px 0 25px;
  margin-bottom: 1rem;
  border-bottom: 2px solid var(--primary-light);
}
#nav-about {
  border-left: 1px solid var(--primary-light);
  border-right: 1px solid var(--primary-light);
}
#nav a {
  font-weight: bold;
  color: var(--link-nav);
  margin: 0;
  padding: 10px 25px;
  list-style: none;
  text-decoration: none;
}
#logo-link {
  padding: 0 !important;
  margin: 0 !important;
}

#navlinks {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-content: center;
  align-items: center;
  text-align: center;
}

#nav a:hover {
    color: var(--link-hover);
}

#nav a.router-link-exact-active {
  color: var(--link-main);
}

@media screen and (max-width:400px) {
  #nav {
    flex-direction: column;
    padding: 0;
    margin: 0;
  }
  #nav a {
    padding: 2px 5px;
    margin: 0;
  }
  #nav-about {
    border-left: none;
    border-right: none;
  }
  #navlinks {
    width: 100%;
    margin: 0 0.5rem;
    padding: 5px;
    overflow: hidden;
  }
  .navlink {
    padding: 5px !important;
  }
}
@media screen and (max-width:250px) {
  nav a {
    font-size: 10pt;
  }
}
</style>
