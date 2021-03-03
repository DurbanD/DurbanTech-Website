<template>
  <div class="home">
    <div id="home-head">
      <img alt="Durban Technology" src="../assets/DurbanTech_Logo_Long_Light_Green_Silver_Closed_T_Spaced_N.png">
    </div>
    <div class="home-content">
      <div class="home-blurb">
        <h3>Welcome to Durban Technology!</h3>
        <p class="home-blurb-paragraph">
          Founded in 2019, DurbanTech is proud to serve our clients locally and nationally. Based out of Oklahoma City, Oklahoma, DurbanTech is commited to providing the best service for the lowest cost for our community, so that you can worry about what is really important. From hardware repair to custom software development, whether you are a small business or an individual, DurbanTech can help make sure your equipment and software is fast, efficient, and exactly what you need.
        </p>
        <p class="info-blurb">
          For more information, visit our <router-link to="/about" class="info-blurb-link">about</router-link> section, or <router-link to="/contact" class="info-blurb-link">contact</router-link> DurbanTech for more information.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
img {
  max-height: 60%;
  max-width: 80%;
}
h3 {
  font-size: 16pt;
  margin-bottom: 1rem;
}
p {
  text-align: left;
  margin: 0.5rem 0.5rem 1rem 1rem;
  font-size: 14pt;
}
.home {
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-content: stretch;
  align-items: center;
  justify-content: flex-start;
  padding: 0;
  margin: 0;
}
.info-blurb {
  text-align: center;
  border-top: 1px solid var(--secondary-bright-semitransparent);
  padding-top: 1rem;
}
#home-head {
  margin: 1rem;
}
.home-content {
  border-radius: 5px;
  padding: 0 30px;
  align-self: center;
  align-items: center;
}
.home-blurb-paragraph {
  padding: 0.5rem;
  text-indent: 3rem;
  line-height: 1.5rem;
}
a {
  color: var(--primary);
}
h1 {
  padding: 0;
  margin: 0;
}

@media screen and (max-width:600px) {
  #app-view {
    width: 90%;
    margin-top: 0.5rem;
  }
}
@media screen and (max-height: 750px) {
  .home-content {
    margin: 0 0.25rem;
    padding: 0.2rem;
  }
}
</style>
