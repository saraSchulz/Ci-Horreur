<script setup></script>

<template>
  <footer>
    <div class="maior">
      <ul>
        <li>
          <a href="https://www.instagram.com/ci.horreur/">
          <i class="mdi mdi-instagram"></i>
          @ci.horreur
          </a>
        </li>
        <li>
          <a href="https://open.spotify.com/playlist/7vrpeoeosmKOt8OJ8xJNZo">
          <i class="mdi mdi-spotify"></i>
          Nossa playlist
          </a>
        </li>
      </ul>
      <ul>
        <li>
          <i class="mdi mdi-email"></i>
          ifc.ci.horreur@gmail.com
        </li>
        <li>
          <i class="mdi mdi-phone-classic"></i>
          +55 (47) 992067618
        </li>
      </ul>
    </div>

  </footer>
</template>

<style scoped>
footer {
  background: linear-gradient(to bottom, #3A3A3A 0%, #191919 100%);
  box-shadow: 0 0 75px rgba(0, 0, 0, 0.8);
  padding: 50px;

  & .maior {
    display: flex;
    justify-content: space-between;

    & p {
      font-size: 25px;
      color: #ffffff;
    }
    & ul {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      margin: 10px 20px;

      & li {
        margin: 20px 10px;
        font-size: 30px;
        & .mdi{
          color: #F81F3E;
        }
      }
    }
    & .central {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;

      & .logoFooter {
        a{
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        margin: 0 0 20px;

        & .logo {
          height: 60px;
        }
        }
        & p {
          font-size: 20px;
        }
      }


      & .direitos {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        margin: 20px 0 0;

        & p {
          font-size: 10px;
        }
      }
    }
  }
}
</style>