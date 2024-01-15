<template>
    <div style="color: white">
        <i
            class="el-icon-menu collapse"
            @click="clickCollapse"
            style="margin: 0 20px 0 40px; float: left"
        ></i>

        <div class="misName">欢迎使用成绩管理系统</div>
        <div style="float: right; margin-right: 16px">
            <!--日期-->
            <div class="font" v-html="day"></div>
            <!--头像-->
            <div class="headerStr">
                <el-avatar
                    v-if="imageUrl != undefined"
                    shape="square"
                    :size="50"
                    :src="$store.state.baseApi + imageUrl"
                    :key="$store.state.baseApi + imageUrl"
                    style="margin-top: 5px"
                ></el-avatar>
            </div>
            <!--用户名-->
            <div
                style="
                    float: right;
                    margin-right: 20px;
                    margin-top: 18px;
                    color: white;
                "
            >
                <el-dropdown trigger="click">
                    <span class="el-dropdown-link">
                        {{ userInfo.realName
                        }}<i class="el-icon-arrow-down el-icon--right"></i>
                    </span>
                    <el-dropdown-menu slot="dropdown">
                        <el-dropdown-item
                            icon="el-icon-setting"
                            @click.native="editPassword"
                        >
                            修改密码</el-dropdown-item
                        >
                        <el-dropdown-item
                            icon="el-icon-switch-button"
                            @click.native="exit"
                        >
                            退出登录</el-dropdown-item
                        >
                    </el-dropdown-menu>
                </el-dropdown>
            </div>
        </div>
        <password ref="edit_password"></password>
    </div>
</template>

<script>
import password from "./password/password";
export default {
    name: "Header",
    data() {
        return {
            userInfo: {},
            day: "",
            firstStr: "",
            imageUrl: "",
        };
    },
    methods: {
        clickCollapse() {
            this.$emit("click_collapse");
        },
        exit() {
            this.$confirm("是否注销当前用户?", "提示", {
                confirmButtonText: "确定",
                cancelButtonText: "取消",
                type: "warning",
            }).then(() => {
                this.$router.push("/login");
                // 退出登录时，清除身份信息
                localStorage.clear();
            });
        },
        editPassword() {
            this.$refs.edit_password.init();
        },

        getHead() {
            const obj = {
                userId: this.userInfo.id,
                level: this.userInfo.level,
            };
            this.axiosHelper
                .get("/api/sms/upload/getHeadImg", { params: obj })
                .then((response) => {
                    this.imageUrl = response.data;
                })
                .catch((e) => {
                    console.log(e);
                    if (
                        e.response == undefined ||
                        e.response.data == undefined
                    ) {
                        this.$message.error({
                            showClose: true,
                            message: e,
                            duration: 5000,
                        });
                    } else {
                        this.$message.error({
                            showClose: true,
                            message: e.response.data,
                            duration: 5000,
                        });
                    }
                });
        },
    },
    created() {
        let today = new Date();
        let weekday = [
            "星期日",
            "星期一",
            "星期二",
            "星期三",
            "星期四",
            "星期五",
            "星期六",
        ];
        let date =
            today.getFullYear() +
            "年 " +
            (today.getMonth() + 1) +
            "月 " +
            today.getDate() +
            "日";
        let week = weekday[today.getDay()];
        this.day = date + "&#x3000;" + week;
    },
    computed: {},
    mounted() {
        this.userInfo = JSON.parse(localStorage.userInfo);
        this.firstStr = this.userInfo.realName.substr(0, 1);
        this.getHead();

        this.userInfo = JSON.parse(localStorage.userInfo);
    },
    components: {
        password,
    },
};
</script>

<style scoped>
/* 旋转的关闭按钮*/
.collapse {
    font-size: 25px;
    float: right;
    line-height: 60px;
    transition: 0.2s;
    transform: rotate(-180deg);
    cursor: pointer;
}
/* 旋转的关闭按钮*/
.collapse:hover {
    transition: 0.2s;
    transform: rotate(180deg);
}
.font {
    font-size: 18px;
    margin-right: 80px;
    line-height: 60px;
    float: left;
}
.image {
    border-radius: 50%;
    vertical-align: top;
    margin-top: 5px;
}
.misName {
    margin-left: 50px;
    float: left;
    font-size: 24px;
    line-height: 60px;
}
.username {
    margin-right: 10px;
    line-height: 62px;
    float: right;
}
.el-dropdown-link {
    font-size: 17px;
    cursor: pointer;
    color: white;
}
.el-icon-arrow-down {
    font-size: 17px;
}
.headerStr {
    float: left;
    margin-right: 12px;
    /* border-radius: 50px; */
    width: 45px;
    height: 45px;
    line-height: 45px;
    text-align: center;
    font-size: 35px;
    color: black;
    font-family: cursive;
}

.upload:hover .imgStyle {
    opacity: 0.2;
}
</style>
