<script>
  import { getDatabase, ref, push } from "firebase/database";
  import Footer from "../components/Nav.svelte";
  import { getStorage, ref as refImage, uploadBytes,getDownloadURL } from "firebase/storage";
  import Nav from "../components/Nav.svelte";
  
let title
let price
let description
let place
let files



const storage = getStorage();
const storageRef = refImage(storage, '/imgs');

// 'file' comes from the Blob or File API
// uploadBytes(storageRef, file).then((snapshot) => {
//   console.log('Uploaded a blob or file!');
// });


function writeUserData(imgUrl) {
  const db = getDatabase();
  push(ref(db, 'items/' ), {
    title,
    price,
    description,
    place,
    insertAt:new Date().getTime(),
    imgUrl
  });
  alert("작성완료 +_+");
  window.location.hash = "/";
}

const uploadFile =async() => {
  const file = files[0]
  const name = file.name;
  const imgRef = refImage(storage, name)
  const res = await uploadBytes(imgRef,file)
  const url = await getDownloadURL(imgRef)
  return url;
}
const handleSubmit =async() => {
  const url = await uploadFile()
  writeUserData(url)
}
</script>

<form id="write-form" on:submit|preventDefault={handleSubmit}>
  
  <div>
    <label for="image">이미지</label>
    <input id="image" name="image" type="file" bind:files={files} />
  </div>
  <div>
    <label for="title">제목</label>
    <input id="title" name="title" type="text" bind:value={title}/>
  </div>
  <div>
    <label for="price">가격</label>
    <input id="price" name="price" type="number" bind:value={price}/>
  </div>
  <div>
    <label for="description">설명</label>
    <input id="description" name="description" type="text" bind:value={description}/>
  </div>
  <div>
    <label for="place">장소</label>
    <input id="place" name="place" type="text" bind:value={place}/>
  </div>
  <div>
    <button class="write-button" type="submit">완료했당께</button>
  </div>
</form>
<Nav location="write"/> 
<style>
  .write-button {
    background-color: tomato; 
    cursor: pointer;
    color:white;
  }
</style>