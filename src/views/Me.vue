<template>
  <v-app>
    <v-container class="profile-container">
      <v-row justify="center">
        <v-col cols="12" md="8">
          <v-card>
            <v-card-title class="justify-center custom-font">{{ profile[language].profile }}</v-card-title>
            <v-img
              src="https://scontent.fbkk27-1.fna.fbcdn.net/v/t39.30808-6/288682938_2655977067880700_7428804885472758011_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=5f2048&_nc_ohc=dXK-gyYonbYQ7kNvgGlP5-I&_nc_ht=scontent.fbkk27-1.fna&oh=00_AYCDe2Esg4BtvgZ1I_6HWQ57r04mkIdT6286spkOP4veUg&oe=666DCE13"
              alt="Profile Picture"
              class="profile-picture"
              aspect-ratio="1"
            ></v-img>
            <v-card-text>
              <div class="text-center">
                <h2>{{ profile[language].name }}</h2>
                <p>{{ profile[language].title }}</p>
                <v-btn class="ma-2" outlined color="primary" @click="toggleLanguage">{{ profile[language].btmenth }}</v-btn>
                <v-btn class="ma-2" color="primary" @click="dialog = true">{{ profile[language].Other }}</v-btn>
              </div>
              <div class="profile-details">
                <v-row>
                  <v-col cols="12" sm="6">
                    <v-icon left>mdi-email</v-icon> {{ profile[language].email }}
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-icon left>mdi-phone</v-icon> {{ profile[language].phone }}
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-icon left>mdi-map-marker</v-icon> {{ profile[language].address }}
                  </v-col>
                  <v-col cols="12" sm="6">
                    <v-icon left>mdi-facebook</v-icon> {{ profile[language].linkedin }}
                  </v-col>
                </v-row>
              </div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>

      <v-dialog v-model="dialog" max-width="600px">
        <v-card>
          <v-card-title class="headline">More Profiles</v-card-title>
          <br/>
          <v-card-text>
            <!-- ใส่ข้อมูลเพิ่มเติมที่นี่ --><cardimg/>
            <br/>
            <p style="font-family: 'Roboto', sans-serif; font-size: 16px; color: black;">จบการศึกษา : </p>
            <p>ประถมศึกษาปีที่ 1 ถึง 6 | โรงเรียนพลวิทยา</p>
            <p>มัธยมศึกษาที่ 1 ถึง 3 | โรงเรียนหาดใหญ่วิทลัยสมบูรณ์กุลกันยา</p>
            <p>ประกาศนียบัตรวิชาชีพ 1 ถึง 3 | วิทยาลัยเทคโนโลยีพณิชยการหาดใหญ่</p>
            <p>ประกาศนียบัตรวิชาชีพชั้นสูง 1 ถึง 2 | วิทยาลัยเทคโนโลยีพณิชยการหาดใหญ่</p>
            <v-icon left>mdi-new-box</v-icon>
            <p>ปริญญาตรีหลักสูตร 2 ปี</p>
            <p>มหาวิทยาลัยสงขลานครินทร์</p>
            <p>คณะ วิทยาศาสตร์</p>
            <p>สาขา เทคโนโลยีสารสนเทศ(ต่อเนื่อง)</p>
            <br/>   
            <p style="font-family: 'Roboto', sans-serif; font-size: 16px; color: black;">งานอดิเรก : </p>
            <p>- เล่นเกมส์กับเพื่อน ๆ </p>
            <p>&nbsp;&nbsp;&nbsp; - Valorant </p>
            <p>&nbsp;&nbsp;&nbsp; - Minecraft </p>
            <p>&nbsp;&nbsp;&nbsp; - TeamFight Tactics[TFT] </p>
            <p>- เล่นกีฬา </p>
            <p>&nbsp;&nbsp;&nbsp; - ตีแบด </p>
            <p>&nbsp;&nbsp;&nbsp; - บาสเกตบอล </p>
            <p>&nbsp;&nbsp;&nbsp; - ปิงปอง </p>
            <p>&nbsp;&nbsp;&nbsp; - ว่ายน้ำ </p>
            <p>&nbsp;&nbsp;&nbsp; - วอลเล่ย์ </p>
            <br/>   
            <p style="font-family: 'Roboto', sans-serif; font-size: 16px; color: black;">สิ่งที่ชอบ : </p>
            <p>- ชอบกินจำพวกเนื้อ เช่น สเต็ก หมูกะทะ ชาบู (แพ้อาหารทะเล) </p>
            <p style="font-family: 'Roboto', sans-serif; font-size: 16px; color: black;">สิ่งที่ไม่ชอบ : </p>
            <p>- แมลง/แมง สัตว์ที่มีหลายขา </p>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialog = false">Close</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-container>
  </v-app>
</template>

<script>


export default {
  name: 'UserProfile',
  data() {
    return {
      dialog: false,
      language: 'EN',  // Default language
      profile: {
        EN: {
          name: "Phichet Mongkontanapipat",
          title: "Software Engineer",
          email: "p.phichet536@gmail.com",
          phone: "+66 611139856",
          address: "103/48 M.7 Tambon KhaoRupChang Amphur MueangSongkhla Province Songkhla",
          linkedin: "facebook.com/peetkint",
          btmenth:"EN/TH",
          Other:"Other",
          profile:"PROFILE"
          
        },
        TH: {
          name: "พิเชษฐ์ มงคลธนพิพัฒน์",
          title: "วิศวกรซอฟต์แวร์",
          email: "p.phichet536@gmail.com",
          phone: "+66 611139856",
          address: "103/48 หมู่ 7 ตำบล เขารูปช้าง อำเภอ เมืองสงขลา จังหวัด สงขลา",
          linkedin: "facebook.com/peetkint",
          btmenth:"อังกฤษ/ไทย",
          Other:"เพิ่มเติม",
          profile:"ประวัติส่วนตัว"
        }
      }
    };
  },
  methods: {
    toggleLanguage() {
      this.language = this.language === 'EN' ? 'TH' : 'EN';
    }
  },
  components: {
    cardimg: () => import('../components/ImgCard.vue')
  }
};
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700&display=swap');

.profile-container {
  margin-top: 50px;
}

.profile-picture {
  border-radius: 50%;
  width: 150px;
  height: 150px;
  margin: auto;
}

.profile-details {
  margin-top: 20px;
}

.custom-font {
  font-family: 'Roboto', sans-serif;
}
</style>
