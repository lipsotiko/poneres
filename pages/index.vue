<template>
  <div class="my-container">
    <div class="one">
      <img
        class="logo"
        src="~/assets/images/poneres-logo.png"
        alt="Poneres.com Logo"
      />
    </div>
    <div class="description-text-container second-col-gridarea two">
      <span class="description-text">A property management company.</span>
    </div>
    <div class="mail-to last-row-alignment four">
      <div>
        <a href="mailto:hello@poneres.com">
          <img
            src="~/assets/images/envelope-solid.svg"
            width="20"
            alt="email icon"
          />
          <div>hello@poneres.com</div>
        </a>
        <a href="tel:443-301-9719">
          <img
            src="~/assets/images/phone-solid.svg"
            width="20"
            alt="phone icon"
          />
          <div>443-301-9719</div>
        </a>
        <a href="http://poneres-portal-landing.s3-website.us-east-1.amazonaws.com" target="_blank">
          <img
            src="~/assets/images/globe.svg"
            width="20"
            alt="phone icon"
          />
          <div>Property Pal</div>
        </a>
      </div>
    </div>
    <div class="second-col-gridarea last-row-alignment three">
      <div class="service-areas">Baltimore - Chicago - Miami</div>
    </div>
  </div>
</template>
<style scoped>
.my-container {
  grid-column-gap: 48px;
  grid-row-gap: 48px;
  flex-direction: column;
  grid-template-rows: auto auto;
  grid-template-columns: 1fr 1fr 1fr;
  grid-auto-columns: 1fr;
  justify-content: space-around;
  align-items: stretch;
  max-width: none;
  padding: 120px 150px 40px;
  display: grid;
  position: absolute;
  top: 0%;
  bottom: 0%;
  left: 0%;
  right: 0%;
}

.my-container {
  @media screen and (max-width: 767px) {
    flex-wrap: nowrap;
    padding-left: 64px;
    padding-right: 64px;
  }
}

.my-container {
  @media screen and (max-width: 991px) {
    flex-flow: column;
    grid-auto-flow: row;
    justify-content: space-around;
    align-items: stretch;
  }
}

.logo {
  height: 168px;
}

.logo {
  @media screen and (max-width: 991px) {
    height: 98px;
  }
}

.second-col-gridarea {
  grid-area: span 1 / span 2 / span 1 / span 2;
}

.description-text {
  font-size: 52px;
  font-weight: lighter;
}

.description-text {
  @media screen and (max-width: 5000px) {
    font-size: 42px;
  }
}

.description-text {
  @media screen and (max-width: 1600px) {
    font-size: 38px;
  }
}

.description-text {
  @media screen and (max-width: 991px) {
    font-size: 28px;
  }
}

.description-text-container {
  @media screen and (max-width: 5000px) {
    margin-top: 50px;
  }
}

.description-text-container {
  @media screen and (max-width: 1600px) {
    margin-top: 54px;
  }
}

.description-text-container {
  @media screen and (max-width: 991px) {
    margin-top: 20px;
  }
}

.last-row-alignment {
  align-self: end;
}

.mail-to a {
  color: #000;
  display: flex;
  font-weight: lighter;
  text-decoration: none;
}

.mail-to a:hover {
  text-decoration: underline;
  text-decoration-thickness: 0.1px;
}

.mail-to div {
  padding: 8px 8px;
}

.service-areas {
  padding: 26px 8px;
  font-weight: lighter;
  text-wrap: nowrap;
}

.my-container {
  @media screen and (max-width: 991px) {
    flex-flow: column;
    grid-auto-flow: row;
    justify-content: space-around;
    align-items: stretch;
    padding-left: 100px;
    padding-right: 100px;
    display: flex;
  }
}

.one {
  @media screen and (max-width: 991px) {
    flex: 0 auto;
    order: 1;
    display: block;
  }
}

.two {
  @media screen and (max-width: 991px) {
    flex: 1;
    order: 2;
    position: relative;
  }
}

.three {
  @media screen and (max-width: 991px) {
    flex: 0 auto;
    order: 3;
    width: 100%;
    display: flex;
    justify-content: center;
  }
}

.four {
  @media screen and (max-width: 991px) {
    order: 4;
    width: 100%;
    display: flex;
    justify-content: center;
  }
}
</style>
