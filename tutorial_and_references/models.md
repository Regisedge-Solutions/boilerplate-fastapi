# Database models 

SQLAlchemy engine
```
import sqlalchemy as db
from sqlalchemy import Column, String, Integer, Date, Table, ForeignKey
from sqlalchemy.orm import relationship

engine = db.create_engine('dialect+driver://user:pass@host:port/db')
```
https://docs.sqlalchemy.org/en/14/core/engines.html#postgresql


SQLAlchemy models
* Model reference 
* Relationships (One-Many, One-One, One-Many)
* Cascading options 

```
class Product(Base):
    __tablename__ = 'products'

    id = Column(Integer, primary_key=True)
    title = Column('title', String(32))
    in_stock = Column('in_stock', Boolean)
    quantity = Column('quantity', Integer)
    price = Column('price', Numeric)
```

Relationships
https://docs.sqlalchemy.org/en/14/orm/relationship_api.html

One to Many 
```
class Article(Base):
    __tablename__ = 'articles'
    id = Column(Integer, primary_key=True)
    comments = relationship("Comment")


class Comment(Base):
    __tablename__ = 'comments'
    id = Column(Integer, primary_key=True)
    article_id = Column(Integer, ForeignKey('articles.id'))
```

One to One 
```
class Person(Base):
    __tablename__ = 'people'
    id = Column(Integer, primary_key=True)
    mobile_phone = relationship("MobilePhone", uselist=False, back_populates="person")

class MobilePhone(Base):
    __tablename__ = 'mobile_phones'
    id = Column(Integer, primary_key=True)
    person_id = Column(Integer, ForeignKey('people.id'))
    person = relationship("Person", back_populates="mobile_phone")
```

Many to Many 
```
students_classes_association = Table('students_classes', Base.metadata,
    Column('student_id', Integer, ForeignKey('students.id')),
    Column('class_id', Integer, ForeignKey('classes.id'))
)

class Student(Base):
    __tablename__ = 'students'
    id = Column(Integer, primary_key=True)
    classes = relationship("Class", secondary=students_classes_association)

class Class(Base):
    __tablename__ = 'classes'
    id = Column(Integer, primary_key=True)
```

Cascading 
https://docs.sqlalchemy.org/en/14/orm/cascades.html
```
save-update: Indicates that when a parent object is saved/updated, child objects are saved/updated as well.
delete: Indicates that when a parent object is deleted, children of this object will be deleted as well.
delete-orphan: Indicates that when a child object loses reference to a parent, it will get deleted.
merge: Indicates that merge() operations propagate from parent to children.
```

## References
https://www.sqlalchemy.org/