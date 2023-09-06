<script setup>
const wallets = ['plast', 'visa', 'p2p', 'fk', 'ym']
const coins = ['bit', 'lite', 'eth']
let walletsArr = []
let coinsArr = []
for (let item of wallets) {
  const path = new URL(`../assets/img/wallets/${item}.png`, import.meta.url).href
  walletsArr.push(path)
}
for (let item of coins) {
  const path = new URL(`../assets/img/coins/${item}.png`, import.meta.url).href
  coinsArr.push(path)
}
</script>

<template>
  <footer class="footer">
    <div class="footer__box">
      <div class="wrapper footer__wallets wallets">
        <img v-for="(item, index) of walletsArr" :key="index" :src="item" alt="wallet" />
      </div>
      <div class="wrapper footer__wallets coins">
        <img v-for="(item, index) of coinsArr" :key="index" :src="item" alt="coin" />
      </div>
    </div>
    <p class="footer__licence">© 2023 Dragon Money. All rights reserved</p>
  </footer>
</template>

<style lang="scss" scoped>
.footer {
  background: linear-gradient(180deg, rgba(24, 26, 37, 0) 0%, #060818 36.46%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 60px;
  padding: 150px 0 15px;
  margin-top: -200px;

  &__box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 24px;
  }
  &__licence {
    color: #fff;
    font-size: 14px;
    font-weight: 400;
    font-family: 'Exo 2';
  }
  .wallets {
    display: flex;
    align-items: flex-end;
    gap: 25px;
  }
  .coins {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 31px;
  }
}
@media (max-width: 1200px) {
  .footer {
    margin-top: -170px;
  }
}
@media (max-width: 992px) {
  .footer {
    margin-top: -15%;
  }
}
@media (max-width: 768px) {
  .footer {
    margin-top: -18%;
  }
}

@media (max-width: 680px) {
  .footer {
    margin-top: -21%;
    .wallets {
      gap: 5px;
    }
  }
}
@media (max-width: 576px) {
  .footer {
    padding: 120px 0 15px;
    gap: 40px;
    .wallets {
      gap: 10px;
      justify-content: center;
      img {
        &:nth-child(1) {
          width: 75px;
        }
        &:nth-child(2) {
          width: 75px;
        }
        &:nth-child(3) {
          width: 75px;
        }
        &:nth-child(4) {
          width: 75px;
        }
        &:nth-child(5) {
          width: 75px;
        }
      }
    }
    .coins {
      gap: 12px;
      img {
        &:nth-child(1) {
          width: 70px;
        }
        &:nth-child(2) {
          width: 70px;
        }
        &:nth-child(3) {
          width: 90px;
        }
      }
    }
  }
}
@media (max-width: 480px) {
  .footer {
    gap: 33px;
    margin-top: -24%;
    &__box {
      gap: 8px;
    }
    .wallets {
      gap: 10px;
      justify-content: center;
      img {
        &:nth-child(1) {
          width: 36px;
        }
        &:nth-child(2) {
          width: 41px;
        }
        &:nth-child(3) {
          width: 44px;
        }
        &:nth-child(4) {
          width: 45px;
        }
        &:nth-child(5) {
          width: 49px;
        }
      }
    }
    .coins {
      gap: 12px;
      img {
        &:nth-child(1) {
          width: 34px;
        }
        &:nth-child(2) {
          width: 31px;
        }
        &:nth-child(3) {
          width: 41px;
        }
      }
    }
    &__licence {
      font-size: 7px;
    }
  }
}
</style>
