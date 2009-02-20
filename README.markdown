Leave room for the Holy Ghost
=============================

Are you going to the RSpec dance?  That cute model's going to be there.  She's been sending me messages all week.  I can't wait to get her out on the floor.  As long as the chaperone doesn't ruin it...

Chaperone
=========

The **Chaperone** will keep your classes safe and responsible.  Hanky panky on the dance floor?  Tight coupling in the corner?  Not on the Chaperone's watch!

Just give him a copy of the guest list.

    Chaperone.separate User, NewsItem

Now just let your classes *try* to get too close:
    
    class User < ActiveRecord::Base
      after_create { |user| NewsItem.create!(:title => "A new user #{user.name} joined!") }
    end

    describe User do
      it "should have a name" do
        User.create!(:name => "Jill").name.should == "Jill"
      end
    end

Then see how far they get.

    1)
    Spec::Mocks::MockExpectationError in 'User should have a name'
    Mock 'NewsItem' received unexpected message :create! with ({:title=>"A new user Jill joined!"})

A little space, please!  No coupling here!

    describe User do
      it "should have a name" do
        NewsItem.stub!(:create!)
        User.create!(:name => "Jill").name.should == "Jill"
      end
    end

No hidden dependencies.  Everything's in plain sight so you don't have to worry about your classes doing anything inappropriate.  And that's how the Chaperone likes it.

(Coming soon.)
