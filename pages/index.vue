<template>
  <v-row>
    <v-col class="text-center">
      <v-row justify="center" align-content="center">
        <v-col>
          <v-card
            class="mx-auto mt-5"
            elevation="11"
            style="max-width: 700px"
            align="center"
          >
            <v-card-title class="justify-center">
              <v-container>
                <a href="http://den3.net">
                  <v-img
                    src="https://i.imgur.com/zd2U1cJ.png"
                  ></v-img>
                </a>
                <h2
                  align="center"
                  class="font-weight-light mt-5"
                  style="color: #585858"
                >
                  勧誘会 特設ページへようこそ
                </h2>
                <a href="http://den3.net">
                  <h2
                    align="center"
                    class="font-weight-light mt-5"
                    style="color: #585858"
                  >
                    サークルHPはこちら
                  </h2>
                </a>
                <v-card>
                  <v-card-text class="mt-5">
                    <h2
                      align="center"
                      class="font-weight-light mt-2"
                      style="color: #585858"
                    >
                      勧誘会の日程: <div v-html="face_to_face" class="mt-3"></div>
                    </h2>
                    <v-divider class="mt-2"></v-divider>
                    <h2
                      align="center"
                      class="font-weight-light mt-5"
                      style="color: #585858"
                    >
                      説明会(Zoom)の日程: <div v-html="zoom_info" class="mt-3"></div>
                    </h2>
                    <v-divider class="mt-2"></v-divider>
                    <h2
                      align="center"
                      class="font-weight-light mt-5"
                      style="color: #585858"
                    >
                      説明会 Zoomリンク: <div v-html="zoom_url" class="mt-3"></div>
                    </h2>
                  </v-card-text>
                </v-card>
                <v-card>
                  <v-card-text class="mt-5">
                    <h2
                      align="center"
                      class="font-weight-light"
                      style="color: #585858"
                    >
                      新しいお知らせ
                    </h2>
                    <h2
                      align="center"
                      class="font-weight-light mt-3"
                      style="color: #585858"
                    >
                      <div v-html="new_info"></div>
                    </h2>
                  </v-card-text>
                </v-card>
                <v-card>
                  <v-card-text class="mt-5">
                    <h2
                      align="center"
                      class="font-weight-light"
                      style="color: #585858"
                    >
                      活動日: 毎週水曜日 21:00 ~
                    </h2>
                    <h2
                      align="center"
                      class="font-weight-light mt-3"
                      style="color: #585858"
                    >
                      (ただし, サークルの活動制限によって変わります.)
                    </h2>
                  </v-card-text>
                </v-card>
              </v-container>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-card elevation="0">
                  <v-card-title class="justify-center">
                    <h2 class="font-weight-light" style="color: #585858">
                      次の活動をしている部員がいます
                    </h2>
                  </v-card-title>
                  <v-card-text>
                    <v-row class="mt-5">
                      <v-col v-for="thing in doThing" :key="thing.title">
                        <v-card
                          style="
                            min-width: 250px;
                            max-width: 300px;
                            height: 350px;
                          "
                        >
                          <v-card-title class="justify-center">
                            <h4
                              class="mt-5 font-weight-light"
                              style="color: #585858"
                              align="center"
                            >
                              {{ thing.title }}
                            </h4>
                          </v-card-title>
                          <v-card-text>
                            <v-container>
                              <v-icon size="100">{{ thing.icon }}</v-icon>
                              <p class="mt-4">{{ thing.message }}</p>
                            </v-container>
                          </v-card-text>
                        </v-card>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-card>
              </v-container>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
export default {
  methods: {
    setData: function(obj){
      this.zoom_info = obj.zoom_info;
      this.zoom_url = obj.zoom_url;
      this.face_to_face = obj.face_to_face;
      this.new_info = obj.new_info;
    }
  },
  created: function() {
    fetch("https://10fu3.github.io/den3welcomepageapi/api.json")
      .then((response) => response.json())
      .then((data) => {
        this.setData(data);
      });

    const a = function (){
      console.log(this.data.zoom_info)
    };
  },
  data: () => ({
    zoom_info: "なし",
    zoom_url: "なし",
    face_to_face: "なし",
    new_info: "なし",
    doThing: [
      {
        icon: "mdi-code-braces-box",
        title: "競技プログラミング",
        message: "AtCoder 緑色を目指して日々鍛錬しています.",
      },
      {
        icon: "mdi-controller-classic",
        title: "ゲーム制作",
        message:
          "Unityを使った、音ゲーの制作や過去にはハッカソンでシューティングゲームの制作を行いました",
      },
      {
        icon: "mdi-server",
        title: "WEBアプリ開発",
        message:
          "部内で使うチャットツールを製作中です.ハッカソンではSNSの制作を過去行いました",
      },
      {
        icon: "mdi-chart-bell-curve-cumulative",
        title: "機械学習研究",
        message:
          "機械学習で使われる仕組みそのものを学び、ハッカソンでは線形回帰やニューラルネットワークを用いた新型ウイルスの感染者の予測を行いました",
      },
    ],
  }),
};
</script>
