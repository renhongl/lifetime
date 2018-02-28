## async 和 await

1. 基本用法

   ```
   async function getPersonInformation() {
   	let obj;
   	console.log('before get');
     	await getPerson().then(data => {
         console.log(data);
         obj = data;
     	});
     	console.log('after get ' + obj.name + ' information');
   }

   function getPerson() {
     return new Promise((resolve, reject) => {
       setTimeout(function() {
       	const p = {
             name: 'lrh',
             age: 18
       	};
         	resolve(p)
       })
     });
   }

   getPersonInformation();
   ```

   ​