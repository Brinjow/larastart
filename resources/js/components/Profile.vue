<style>
.widget-user-header {
    background-position : center center;
    background-size : cover;
}

.widget-user .widget-user-header {
    padding: 1rem;
    height: 231px !important;

}
</style>

<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-12 mt-5">
            <div class="card card-widget widget-user">
              <!-- Add the bg color to the header using any of the bg-* classes -->
              <div class="widget-user-header text-white" style="background: url('./img/user-cover.png') center center;">
                <h3 class="widget-user-username">Elizabeth Pierce</h3>
                <h5 class="widget-user-desc">Web Designer</h5>
              </div>
              <div class="widget-user-image">
                <img class="img-circle" src="" alt="User Avatar">
              </div>
              <div class="card-footer">
                <div class="row">
                  <div class="col-sm-4 border-right">
                    <div class="description-block">
                      <h5 class="description-header">3,200</h5>
                      <span class="description-text">SALES</span>
                    </div>
                    <!-- /.description-block -->
                  </div>
                  <!-- /.col -->
                  <div class="col-sm-4 border-right">
                    <div class="description-block">
                      <h5 class="description-header">13,000</h5>
                      <span class="description-text">FOLLOWERS</span>
                    </div>
                    <!-- /.description-block -->
                  </div>
                  <!-- /.col -->
                  <div class="col-sm-4">
                    <div class="description-block">
                      <h5 class="description-header">35</h5>
                      <span class="description-text">PRODUCTS</span>
                    </div>
                    <!-- /.description-block -->
                  </div>
                  <!-- /.col -->
                </div>
                <!-- /.row -->
              </div>
            </div>
            </div>

            <div class="col-md-12 mt-3">
            <div class="card">
              <div class="card-header p-2">
                <ul class="nav nav-pills">
                  <li class="nav-item"><a class="nav-link active show" href="#activity" data-toggle="tab">Activity</a></li>
                  <li class="nav-item"><a class="nav-link" href="#settings" data-toggle="tab">Settings</a></li>
                </ul>
              </div><!-- /.card-header -->
              <div class="card-body">
                <div class="tab-content">
                  <div class="tab-pane active show" id="activity">
                    
                  </div>
                  <!-- /.tab-pane -->

                  <div class="tab-pane" id="settings">
                    <form class="form-horizontal">
                      <div class="form-group">
                        <label for="inputName" class="col-sm-2 control-label">Name</label>

                        <div class="col-sm-12">
                          <input v-model="form.name" type="email" class="form-control" id="inputName" placeholder="Name">
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="inputEmail" class="col-sm-2 control-label">Email</label>

                        <div class="col-sm-12">
                          <input v-model="form.email" type="email" class="form-control" id="inputEmail" placeholder="Email">
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="inputExperience" class="col-sm-2 control-label">Experience</label>

                        <div class="col-sm-12">
                          <textarea class="form-control" id="inputExperience" placeholder="Experience"></textarea>
                        </div>
                      </div>
                      <div class="form-group">
                        <label for="profilephoto" class="col-sm-12 control-label">Profile Photo</label>
                        <div class="input-group col-sm-12">
                            <div class="custom-file">
                                <input @change="updateProfile" type="file" class="custom-file-input" id="exampleInputFile">
                                <label class="custom-file-label" for="exampleInputFile">Choose file</label>
                            </div>
                            <div @change="updateProfile" class="input-group-append">
                                <span class="input-group-text" id="">Upload</span>
                            </div>
                        </div>
                      </div>
                     <div class="form-group">
                        <label for="exampleInputPassword1" class="col-sm-12 control-label">Password (leave empty if not changing)</label>
                        <div class="col-md-12">
                            <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
                        </div>
                    </div>
                      <div class="form-group">
                        <div class="col-sm-offset-2 col-sm-12">
                          <button @click.prevent="updateIfo" type="submit" class="btn btn-success">Update</button>
                        </div>
                      </div>
                    </form>
                  </div>
                  <!-- /.tab-pane -->
                </div>
                <!-- /.tab-content -->
              </div><!-- /.card-body -->
            </div>
            </div>

        </div>
    </div>
</template>



<script>
    export default {
        data() {
            return {
                form: new Form({
                    id : '',
                    name : '',
                    email : '',
                    password : '',
                    type : '',
                    bio : '',
                    profile : ''
                })
            }
        },

        methods : {
            updateIfo() {
                this.form.put('api/profile/')
                .then(()=>{

                })
                .catch(()=>{
                    
                })
            },

            updateProfile(e) {
                let file = e.target.files[0];
                let reader = new FileReader();
                reader.onloadend = (file) => {
                    this.form.photo = reader.result;
                }

                reader.readAsDataURL(file);
            }
        },

        created() {
            axios.get("api/profile")
            .then(({ data }) => (this.form.fill(data)));
        }
      
    }
</script>
