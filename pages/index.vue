<template>
  <div>
    <section v-if="allSurveys">
      <ul>
        <li v-for="survey in allSurveys" :key="survey.name">
          <nuxt-link :to="{
			  name: 'survey-name',
			  params: {name: survey.name }
			  }" class='link'>
            <h3>{{survey.name}}</h3>
		</nuxt-link>
        </li>
      </ul>
    </section>
    <h2 v-else>
      Loading...
    </h2>
  </div>
</template>

<script>
  import gql from 'graphql-tag'

  const allSurveys = gql`
    query {
      allSurveys {
        name
    }
}
  `

  export default {
    name: 'HomePage',
    data: () => ({
      loading: 0
    }),
    apollo: {
      $loadingKey: 'loading',
      allSurveys: {
        query: allSurveys
      }
    }
  }
</script>

<style scoped>
  ul {
    padding: 0;
  }
  li {
    display: flex;
    align-items: center;
    margin-bottom: 16px;
    border: 1px solid #eee;
    overflow: hidden;
    border-radius: 5px;
  }
  .link {
    color: #000;
	display: inline-block;
	width: 100%;
	padding: 8px;
  }
  .link:hover {
    box-shadow: 1px 1px 5px #999;
  }
  img {
    display: block;
    height: 100%;
  }
  .show-more-wrapper {
    display: flex;
    justify-content: center;
  }
  button {
    width: 100%;
    font-size: 16px;
    color: white;
    text-transform: uppercase;
    font-weight: bold;
    padding: 16px 24px;
    background: deepskyblue;
    border: none;
    border-radius: 0;
    cursor: pointer;
  }
</style>
