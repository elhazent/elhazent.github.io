---
layout: post
title: Live Template Untuk Recycler View di Android Studio
date: 2019-04-16 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: android-studio-01.png # Add image post (optional)
tags: [Productivity, Software] # add tag
---

Berkat Live Templates, pengembangan Android lebih cepat dari sebelumnya. Mereka membantu kita menulis kode yang tidak terlalu membosankan dan lebih fokus pada hal-hal terpenting. Mari kita buat template langsung untuk Adaptor RecyclerView.


1. Ketik cmd + shift + A(Mac), ctrl + shift + a(Windows/linux) untuk menapilkan Pencarian.

![Macbook]({{site.baseurl}}/assets/img/template.PNG)
 
2. Ketik di pencarian "add template" lalu tekan enter, maka akan muncul tampilan preference File and Code Template.

![Macbook]({{site.baseurl}}/assets/img/template-3.PNG)

3. Tekan tombol " + " untuk menambahkan templat baru. Lalu beri nama "RecyclerView Adapter" dan tambahkan kode berikut ke dalam kotak nomor 3:

	 #if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
	 #parse("File Header.java")
	 public class ${NAME} extends
        	RecyclerView.Adapter<${NAME}.ViewHolder> {
    	 private static final String TAG = ${NAME}.class.getSimpleName();
    	 private Context context;
    	 private List<${LIST_MODEL}> list;
    	 private OnItemClickListener onItemClickListener;
    	 public ${NAME}(Context context, List<${LIST_MODEL}> list,
     	 OnItemClickListener onItemClickListener) {
        	this.context = context;
        	this.list = list;
        	this.onItemClickListener = onItemClickListener;
    	 }
    	 public static class ViewHolder extends RecyclerView.ViewHolder {
       	 // Todo Butterknife bindings
        	public ViewHolder(View itemView) {
            	super(itemView);
            	ButterKnife.bind(this, itemView);
        	}
        	public void bind(final ${LIST_MODEL} model,
                         	final OnItemClickListener listener) {
            	itemView.setOnClickListener(new View.OnClickListener() {
                	@Override
                	public void onClick(View v) {
                    	listener.onItemClick(getLayoutPosition());
                	}
            	});
        	}
    	 }
    	 @Override
    	 public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        	Context context = parent.getContext();
        	LayoutInflater inflater = LayoutInflater.from(context);
        	View view = inflater.inflate(R.layout.${item_layout}, parent, false);
        	ButterKnife.bind(this, view);
        	ViewHolder viewHolder = new ViewHolder(view)
    	    return viewHolder;
    	 }
    	 @Override
    	 public void onBindViewHolder(ViewHolder holder, int position) {
        	${LIST_MODEL} item = list.get(position);
        	//Todo: Setup viewholder for item 
        	holder.bind(item, onItemClickListener);
    	 }
    	 @Override
    	 public int getItemCount() {
         return list.size();
    	 }
    	 public interface OnItemClickListener {
         void onItemClick( int position);
    	 }
	}


Lalu Click **OK**

Itu dia! Anda baru saja menambahkan Live Template pertama Anda! Mari kita coba:

1. Pergi ke Project
2. lalu pilih package project kita
3. click kanan pada project kita
4. kita pilih New
5. maka kita akan melihat class RecyclerViewAdapter , lalu kita click.

![Macbook]({{site.baseurl}}/assets/img/template-4.PNG)

6. setelah itu maka akan muncul pop up seperti berikut.

![Macbook]({{site.baseurl}}/assets/img/template-5.PNG)


7. Tuliskan nama adapter baru Anda ke dalam Nama file, contoh MahasiswaAdapter

8. Tuliskan nama kelas Model Anda, misal Mahasiswa

9. Tuliskan nama tata letak Anda, mis. mahasiswa_recycler_adapter

Itu dia! Nikmati pengembangan Android menggunakan Live Template! Saya berharap dapat melihat lebih banyak templat dari pengembang Android lainnya!