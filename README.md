## Rails CRUD

### 1. ORM (Object Relational Mapper)
- Rails에서는 [ActiveRecord](https://guides.rorlab.org/active_record_basics.html)를 활용한다.
### 2. Controller 생성
```bash
$ rails g controller post index new create show edit update destroy
```
### 3. Model 생성
```bash
$ rails g model post
```
  - `app/model/post.rb`
  - `db/migrate/20180619_create_posts.rb`
- `migration 파일` 변경
```ruby
# db/migrate/migrate/20180619_create_posts.rb
class CreatePosts < ActiveRecord::Migration
  def change
    create_table :posts do |t|
      t.string :title
      t.text :body
      t.timestamps null: false
    end
  end
end
```

```bash
$rake db:migrate
#진짜 table을 만든다
== 20180619043119 CreatePosts: migrating ======================================
-- create_table(:posts)
   -> 0.0089s
== 20180619043119 CreatePosts: migrated (0.0098s) =============================

```
  - `db/schema.rb`에 반영이 되었는지 확인


## CRUD
  - Create : `new`, `create`
  - Read : `show`
  - Update : `edit`, `update`
  - Destroy : `destroy`

- Create
```bash
> Post.create(title:"제목", body:"내용")
```

- Read
```bash
> Post.find(id)
```
- update
```bash
> post = Post.find(id)
> post.update(title:"제목 수정", body:"내용 수정")
```

- Destroy
```bash
> Post.find(id).destroy
```

## [Rails flash message](https://guides.rorlab.org/action_controller_overview.html#flash)

```ruby
def destroy
  flash[:alert] = "삭제되었습니다."
end
```
```erb
<%= flash[:alert]%>
```

## [Rails partial](https://guides.rorlab.org/layouts_and_rendering.html#%ED%8C%8C%EC%85%9C-partial-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

`app/views/layout/_flash.html.erb`
```erb
<%= render 'layout/flash'%>
```
