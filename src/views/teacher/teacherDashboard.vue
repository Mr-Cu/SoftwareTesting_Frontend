<template>
  <v-app id="inspire">
    <v-container>
      <v-row>
        <v-col cols="12" sm="7">
          <v-row>
          <v-card class="mx-4 rounded-xl pa-4"  :elevation=10>
            <v-row>
              <v-col cols="12" sm="4">
                <v-img src="@/assets/teacher1.png" class="mt-n20"></v-img>
              </v-col>
              <v-col cols="12" sm="8">
                <v-list-item three-line>
                  <v-list-item-content>
                    <v-list-item-title class="text-h4 mb-1">
                      老师您好！
                    </v-list-item-title>
                    <v-divider></v-divider>
                    <v-list-item-subtitle
                      >欢迎来到TJLMS实验教学平台<br />
                    </v-list-item-subtitle>
                  </v-list-item-content>
                </v-list-item>
                <v-card-actions>
                  <router-link to='/teacherLab'>
                  <v-btn
                    class="px-3"
                    color="green"
                    dark
                    style="margin-left: 30px"

                  >
                    进入实验管理
                  </v-btn>
                  </router-link>
                  <router-link to='/teacherClass'>
                  <v-btn
                    class="px-3"
                    color="green"
                    dark
                    style="margin-left: 30px"
                  >
                    我的班级
                  </v-btn>
                  </router-link>
                </v-card-actions>
              </v-col>
            </v-row>
          </v-card>
          </v-row>
          <v-row>
            <v-col cols="12" sm="8">
              <h2 class="font">课程信息</h2>
        <v-card class="mx-auto" max-width="600">
          <v-img
            src="https://globbsecurity.com/wp-content/uploads/2019/05/wan.jpg"
            height="200px"
            class="white--text align-end"
          >
            <v-card-title style="font-size: 25px; font-weight: bold">
              计算机组成原理实验
            </v-card-title>
            <v-card-subtitle> 国家级精品课程 </v-card-subtitle>
          </v-img>

          <v-card-text class="text--primary">
            <div>主讲老师：黄杰</div>
            <div>开课学期：2021-2022 秋季学期</div>
            <div>学时：34{{ "\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0" }}学分：2</div>
          </v-card-text>

          <v-card-actions>
            <v-btn color="purple" text @click="show = !show">
              查看详情 Explore more
            </v-btn>

            <v-spacer></v-spacer>

            <v-btn icon @click="show = !show">
              <v-icon>{{
                show ? "mdi-chevron-up" : "mdi-chevron-down"
              }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>
              <v-card-text>
                同济大学计算机组成原理配套实验
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
            </v-col>
          </v-row>
        </v-col>

        <v-col cols="12" sm="4" style="margin-left:30px">
          <v-card class="mx-4 rounded-xl pa-4" color="grey lighten-3" :elevation=10>
            <template>
              <v-card class="mx-auto rounded-xl" max-width="434" tile >
                <v-img >
                      <v-row
                   align="end"
                   class="pa-3"
                   sm="4"
                  >
                    <v-col
                     align-self="start"
                     class="px-3"
                     cols="12"
                     sm="4"
                    >
                      <v-avatar class="profile" style="box-shadow: 0px 2px 12px #A3A3A3;" color="grey" size="90" :elevation=20 >
                        <v-img src="@/assets/teacher.png" ></v-img>
                      </v-avatar>
                  </v-col>

                  <v-col class="pb-4 pl-3" sm="8" style="padding-right:0px;">
                  <v-list-item color="black" class="py-0">
                    <v-list-item-content >
                      <v-list-item-title class="title" ><span style="font-size:18px;"> {{name}} </span></v-list-item-title>
                       <div style="font-size:6px;">&nbsp;</div>
                      <v-list-item-subtitle style="font-size:13px;">
                        {{role}}
                        </v-list-item-subtitle>
                    </v-list-item-content>
                   </v-list-item>
                  </v-col>
                 </v-row>

               </v-img>
             </v-card>
        </template>
      </v-card>
    </v-col>
  </v-row>
</v-container>
</v-app>
</template>

<script>

export default {
  name: 'Home',
  data: () => ({
    show: false,
    name: JSON.parse(sessionStorage.getItem('detail')).name,
    role: ''
  }),
  methods: {
    getRole () {
      const type = JSON.parse(sessionStorage.getItem('detail')).type
      switch (type) {
        case 0:
        {
          this.role = '责任教师 软件学院'
          break
        }
        case 1:
        {
          this.role = '普通教师 软件学院'
          break
        }
        case 2:
        {
          this.role = '助教 软件学院'
          break
        }
      }
    }
  },
  created () {
    this.getRole()
  }
}
</script>

<style scoped>
.font {
  color: rgb(2, 160, 160) ;
}
</style>
