<template>
  <div>
    <h1>issueリスト</h1>
    <el-button type="success" @click="getIssues()">issue取得</el-button>
    <el-row gutter="10">
      <el-col :span="12" v-for="issue in issueData" :key="issue.id">
        <el-card class="box-card">
          {{ issue.title }}
          <el-button @click='closeIssue(issue.number)' type="success" icon="el-icon-check" circle></el-button>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios';

const client = axios.create({
  baseURL: `${process.env.VUE_APP_GITHUB_ENDPOINT}`,
  headers: {
    'Accept': 'application/vnd.github.v3+json',
    'Content-Type': 'application/json',
    'Authorization': `token ${process.env.VUE_APP_GITHUB_TOKEN}`
  },
});

export default {
  name: 'IssueList',
  data() {
    return {
      issueData: [],
    }
  },
  methods: {
    getIssues() {
      client.get('/issues')
        .then((res) => { this.issueData = res.data; });
    },
    closeIssue(number) {
      client.patch(`/issues/${number}`, { state: 'closed' })
        .then(
          (number) => { this.issueData.splice(number - 1, 1); }
        );
    },
  },
  created() {
    this.getIssues();
  }

}
</script>