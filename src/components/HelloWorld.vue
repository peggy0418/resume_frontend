<template>
  <div class="resume">
    <header>
      <h1>{{ personalInfo.name }}</h1>
      <p>{{ personalInfo.jobTitle }}</p>
    </header>

    <section>
      <h2>基本資料</h2>
      <ul>
        <li><strong>電子郵件:</strong> {{ personalInfo.email }}</li>
        <li><strong>手機:</strong> {{ personalInfo.phone }}</li>
        <li><strong>地址:</strong> {{ personalInfo.address }}</li>
      </ul>
    </section>

    <section>
      <h2>學歷</h2>
      <ul>
        <li v-for="edu in education" :key="edu.id">
          <h3>{{ edu.degree }}</h3>
          <p>{{ edu.school }}</p>
          <p>{{ edu.year }}</p>
        </li>
      </ul>
    </section>

    <section>
      <h2>工作經歷</h2>
      <ul>
        <li v-for="exp in experience" :key="exp.id">
          <h3>{{ exp.position }}</h3>
          <p>{{ exp.company }}</p>
          <p>{{ exp.year }}</p>
          <p>{{ exp.description }}</p>
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
const personalInfo = {
  name: "張珮綺",
  jobTitle: "前端工程師-實習生",
  email: "but5863841@email.com",
  phone: "0908-585-010",
  address: "台中市 龍井區",
};

const education = [
  {
    id: 1,
    degree: "學士",
    school: "國立雲林科技大學",
    year: "2019-2022",
  },
  // Add more education entries as needed
];

const experience = [
  {
    id: 1,
    position: "前端工程師-實習生",
    company: "Monosparta",
    year: "2023/7-現在",
    description: "",
  },
  // Add more work experience entries as needed
];
</script>

<style>
.resume {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

header {
  text-align: center;
  margin-bottom: 20px;
}

h1 {
  font-size: 2rem;
  margin: 0;
}

p {
  font-size: 1rem;
  margin: 0;
}

section {
  margin-bottom: 20px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}
</style>
