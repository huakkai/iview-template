<style scoped>
.layout{
    border: 1px solid #d7dde4;
    background: #f5f7f9;
    position: relative;
    border-radius: 4px;
    overflow: hidden;
}
.layout-logo{
    width: 100px;
    height: 30px;
    background: #5b6270;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 15px;
    left: 20px;
}
.layout-nav{
    width: 420px;
    margin: 0 auto;
    margin-right: 20px;
}
.layout-footer-center{
    text-align: center;
}
</style>
<template>
    <div class="layout">
        <Layout>
            <Header>
                <Menu mode="horizontal" theme="dark" active-name="1">
                    <div class="layout-nav">

                    </div>
                </Menu>
            </Header>
            <Content :style="{padding: '0 50px'}">
                <Breadcrumb :style="{margin: '20px 0'}">
                    <BreadcrumbItem>Chat Room</BreadcrumbItem>
                </Breadcrumb>
                <Card>
                    <Form ref="formCustom" :model="formCustom" :rules="ruleCustom" :label-width="80">
                        <FormItem prop="message">
                          <Input v-model="formCustom.textarea" type="textarea" :rows="16"></Input>
                        </FormItem>
                        <FormItem prop="info">
                            <Input type="text" v-model="formCustom.info" placeholder="Enter something..."></Input>
                        </FormItem>
                        <FormItem>
                            <Button type="primary" @click="handleSubmit('formCustom')">Submit</Button>
                            <Button @click="handleReset('formCustom')" style="margin-left: 8px">Reset</Button>
                        </FormItem>
                    </Form>
                </Card>
            </Content>
            <Footer class="layout-footer-center">2011-2016 &copy; TalkingData</Footer>
        </Layout>
    </div>
</template>

<script>
    export default {
        data () {
            const validateInfo = (rule, value, callback) => {
                if (!value) {
                    return callback(new Error('cannot be empty'));
                }
            };

            return {
                formCustom: {
                    info: '',
                    message: '',
                },
                ruleCustom: {
                    info: [
                        { validator: validateInfo, trigger: 'blur' }
                    ]
                }
            }
        },
        methods: {
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('Submit Success!');
                    } else {
                        this.$Message.error('Submit Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            }
        }
    }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
