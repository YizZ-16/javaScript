

var imageResizer = function (ofile, callback) {
    // if (/^image\/\w+/.test(ofile.type)) {
    //     alert("请上传图片");
    //     return
    // }
    let size = ofile.size;
    if (size>3.5*1024*1024) {
        alert("图片过大，不能上传");
        return
    }
    if (size>1024*1024-1) {
        compress(ofile, 0.3, callback);
        return
    }
    if (size>500*1024-1) {
        compress(ofile, 0.5, callback);
        return
    }
    if (size < 500 * 1024) {
        if (callback) {
            callback(ofile)
        }
    }

};

function dataURLtoBlob(dataurl) {
    var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while(n--){
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new Blob([u8arr], {type:mime});
}

function compress(ofile, quality, callback) {
    let reader = new FileReader();
    reader.readAsDataURL(ofile);
    reader.onload = function (image) {
        let base64Img = image.target.result;
        let old = new Image();
        old.src = base64Img;
        old.onload = function () {
            let cvs = document.createElement('canvas');
            cvs.width = 400//old.naturalWidth;
            cvs.height = 400 //old.naturalHeight;
            let ctx = cvs.getContext('2d').drawImage(old, 0, 0,old.naturalWidth,old.naturalHeight, 0,0, 400, 400);
            let newImg = cvs.toDataURL('image/png',quality)
            let blob = dataURLtoBlob(newImg);
            //new Image().src = newImg;
           //  console.log(blob)
            //blob.name=ofile.name;
            callback(blob)
          //  return blob;
        }
    }
}
